# Install software
```bash
git clone https://github.com/sonnyyu/docker-splunk-hec
cd docker-splunk-hec
```
# Get Server Certificate "server.pem"
Use mtls-cert-manage generate server/client/ca certificate 

[https://github.com/sonnyyu/mtls-cert-manage](https://github.com/sonnyyu/mtls-cert-manage)

# Make server.pem
```bash
cd ~/mtls-cert-manage
export serverip="192.168.1.204"
easy-rsa --subject-alt-name="DNS:localhost,IP:$serverip"  build-server-full $serverip nopass
export workdir=~/mtls-cert-manage
sudo -E cp $workdir/pki/pki/private/$serverip.key  $workdir/cert
sudo -E cp $workdir/pki/pki/issued/$serverip.crt $workdir/cert
sudo -E cp $workdir/pki/pki/ca.crt $workdir/cert 
cd $workdir/cert
sudo chmod 644  *
# add password into private key
openssl rsa -aes256 -in $serverip.key -out $serverip.pw.key
# convert crt to pem
openssl x509 -inform PEM -in $serverip.crt > $serverip.pem
# genarate server.pem
cat $serverip.pem $serverip.key ca.crt > server.pem
```
# show server crt file
```bash
openssl x509 -in  $serverip.crt -text
```
# Copy Certificate from mtls-cert-manage
```bash
cd ~/mtls-cert-manage/cert 
cp ca.crt server.pem ~/docker-splunk-hec/splunk/certs
```
# Build Splunk docker image
```bash
docker-compose build
```
# Getting Splunk started 
```bash
docker-compose up -d
```
# Quit 
```bash
docker-compose down 
```
# Quit and remove Volume
```bash
docker-compose down -v
```
# Test web interface
```bash
wget http://192.168.1.204:8000
```
# Open Splunk from Browser
```bash
http://192.168.1.204:8000
```
# Allows curl to proceed and operate even for server connections otherwise considered insecure
```bash
curl -k "https://192.168.1.204:8088/services/collector" \
    -H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
    -d '{"event": "Hello, world!", "sourcetype": "manual"}'
```
# Add the CA cert for your server to the existing default CA certificate store (CURL)
```bash
curl --cacert ca.crt  "https://192.168.1.204:8088/services/collector" \
-H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
-d '{"event": "Hello, world!", "sourcetype": "manual"}'
```
# After install ca.crt into CA certificate store (OS)
```bash
curl  "https://192.168.1.204:8088/services/collector" \
    -H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
    -d '{"event": "Hello, world!", "sourcetype": "manual"}'
```

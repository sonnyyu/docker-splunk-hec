# Install software
```bash
git clone https://github.com/sonnyyu/docker-splunk-hec
cd docker-splunk-hec
```
# Get Server Certificate "server.pem"
Use mtls-cert-manage generate server/client/ca certificate 

[https://github.com/sonnyyu/mtls-cert-manage](https://github.com/sonnyyu/mtls-cert-manage)


# Copy Certificate from mtls-cert-manage
```bash
cd ~/mtls-cert-manage/pki/splunkcerts
cp ca.crt server.pem ~/docker-splunk-hec/splunk/certs
sudo cp 192.168.1.204.pem 192.168.1.204.key ~/docker-splunk-hec/splunk/webcerts
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
wget https://192.168.1.204:8000 -O /tmp/index.html
```
# Open Splunk from Browser
```bash
https://192.168.1.204:8000
```
# Allows curl to proceed and operate even for server connections otherwise considered insecure
```bash
curl -k "https://192.168.1.204:8088/services/collector" \
    -H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
    -d '{"event": "Hello, world!", "sourcetype": "manual"}'
```
# Add the CA cert for your server to the existing default CA certificate store (CURL)
```bash
cd ~/docker-splunk-hec/splunk/certs
curl --cacert ca.crt  "https://192.168.1.204:8088/services/collector" \
-H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
-d '{"event": "Hello, world!", "sourcetype": "manual"}'
```
# Import CA certificate at PC
[Install certificate](https://github.com/sonnyyu/mtls-cert-manage#install-certificate-at-windows)

# After install ca.crt into CA certificate store (OS)
```bash
curl  "https://192.168.1.204:8088/services/collector" \
    -H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
    -d '{"event": "Hello, world!", "sourcetype": "manual"}'
```

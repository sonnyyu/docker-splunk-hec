# Install software
```bash
git clone https://github.com/sonnyyu/docker-splunk-hec
cd docker-splunk-hec
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
# Open Splunk from Browser
```bash
curl  "https://192.168.1.204:8088/services/collector" \
    -H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" \
    -d '{"event": "Hello, world!", "sourcetype": "manual"}'
```

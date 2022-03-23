# Install software
```bash
git clone https://github.com/sonnyyu/docker-splunk-hec
cd docker-splunk-hec
```
# Build Splunk docker image
```bash
docker-compose build
```
# Getting started portainer with certificate
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
wget https://192.168.1.204:8000
```
# Open Splunk from Browser
```bash
https://192.168.1.204:8000
```


docker-compose config

docker-compose up --build

docker-compose stop

docker-compose up -d

docker logs splunk

docker-compose down

docker container prune -f

docker image prune -a -f

docker volume prune -f

docker network prune -f

docker system prune -f

sudo rm -rf /var/lib/docker/volumes/*

docker exec -it docker-splunk /bin/bash

curl -k  https://10.145.89.1:8088/services/collector/event -H "Authorization: Splunk 3f066d2a-c871-4800-87fc-e6be5fa69f1b" -d '{"event": "hello world"}'

{"text": "Success", "code": 0}

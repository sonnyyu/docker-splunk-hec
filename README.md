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
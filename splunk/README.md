
docker build -t sonnyyu/splunk .

docker run -d -p 8000:8000 -e 'SPLUNK_START_ARGS=--accept-license' -e 'SPLUNK_PASSWORD=password' sonnyyu/splunk:latest

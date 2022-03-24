FROM splunk/splunk:latest
USER root
LABEL maintainer "sonnyyu123@gmail.com"
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
COPY inputs.conf /opt/splunk/etc/apps/launcher/local/inputs.conf
COPY splunk_httpinput/inputs.conf /opt/splunk/etc/apps/splunk_httpinput/local/inputs.conf
COPY certs/server.pem  /opt/splunk/etc/auth/

FROM splunk/splunk:latest
USER root
LABEL maintainer "sonnyyuirm@gmail.com"
RUN ln -fs /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata
COPY inputs.conf /opt/splunk/etc/apps/launcher/local/inputs.conf
COPY ginputs.conf /opt/splunk/etc/apps/splunk_httpinput/local/inputs.conf

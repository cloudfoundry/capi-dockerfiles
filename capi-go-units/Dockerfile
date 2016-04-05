FROM golang
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN apt-get update && \
    apt-get install unzip && \
    apt-get clean

RUN wget -q https://releases.hashicorp.com/consul/0.5.2/consul_0.5.2_linux_amd64.zip -P /tmp/ && \
    unzip /tmp/consul_0.5.2_linux_amd64.zip -d /usr/local/bin && \
    rm /tmp/consul_0.5.2_linux_amd64.zip

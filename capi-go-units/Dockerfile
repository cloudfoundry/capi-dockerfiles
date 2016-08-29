FROM golang
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN set -ex \
    && apt-get update \
    && apt-get install unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q https://releases.hashicorp.com/consul/0.6.4/consul_0.6.4_linux_amd64.zip -P /tmp/ && \
    unzip /tmp/consul_0.6.4_linux_amd64.zip -d /usr/local/bin && \
    rm /tmp/consul_0.6.4_linux_amd64.zip

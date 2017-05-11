FROM ruby:2.3
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN \
  apt-get update && \
  apt-get -y install \
    build-essential \
    curl \
    jq \
    mercurial \
    software-properties-common \
    wget \
    apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
    && curl -fSL -o /usr/local/bin/bosh-init \
        "https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-0.0.92-linux-amd64" \
    && chmod 0755 /usr/local/bin/bosh-init

RUN wget "$(curl -s https://api.github.com/repos/cloudfoundry/bosh-bootloader/releases | jq -r 'map(select((.prerelease == false) and (.draft == false) and (.tag_name|startswith("v3"))))[0].assets[].browser_download_url' | grep _linux)" && \
  mv bbl-* /usr/local/bin/bbl && \
  chmod +x /usr/local/bin/bbl

ENV GOPATH $HOME/go
ENV PATH $HOME/go/bin:/usr/local/go/bin:$PATH
RUN \
  wget https://storage.googleapis.com/golang/go1.6.2.linux-amd64.tar.gz -P /tmp && \
  tar xzvf /tmp/go1.6.2.linux-amd64.tar.gz -C /usr/local && \
  mkdir $GOPATH && \
  rm -rf /tmp/*

RUN go get github.com/square/certstrap

RUN echo "deb https://packages.cloud.google.com/apt cloud-sdk-$(lsb_release -c -s) main" >> \
  /etc/apt/sources.list.d/google-cloud-sdk.list && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
  apt-get update && \
  apt-get -y install google-cloud-sdk && \
  apt-get clean

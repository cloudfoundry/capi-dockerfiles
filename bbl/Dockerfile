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
    unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
    && curl -fSL -o /usr/local/bin/bosh-init \
        "https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-0.0.92-linux-amd64" \
    && chmod 0755 /usr/local/bin/bosh-init

RUN wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v3.2.3/bbl-v3.2.3_linux_x86-64 && \
  mv bbl-* /usr/local/bin/bbl && \
  chmod +x /usr/local/bin/bbl

RUN wget -O /tmp/terraform.zip https://releases.hashicorp.com/terraform/0.9.6/terraform_0.9.6_linux_amd64.zip && \
  unzip /tmp/terraform.zip -d /usr/local/bin/ && \
  rm /tmp/terraform.zip

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

FROM ubuntu:trusty

ENV bosh_cli_version 5.4.0
ENV bbl_version 6.6.7
ENV credhub_cli_version 1.7.7
ENV go_version 1.11.4

RUN \
  echo "****** This is my working directory ******" && \
  pwd && \
  echo && \
  echo "++++++ Here's what's in my root directory ++++++++" && \
  ls -hla --color=tty && \
  echo && \
  echo "====== Here's what's one step above me ======" && \
  ls -hla .. && \
  echo

RUN \
  apt-get update && \
  apt-get -y install \
    build-essential \
    wget \
    curl \
    openssh-client \
    software-properties-common \
    unzip

RUN \
  add-apt-repository ppa:git-core/ppa -y && \
  apt-get update && \
  apt-get install -y git && \
  apt-get remove -y --purge software-properties-common

ENV GOPATH /go
ENV PATH /go/bin:/usr/local/go/bin:$PATH
RUN \
  wget https://storage.googleapis.com/golang/go${go_version}.linux-amd64.tar.gz -P /tmp && \
  tar xzvf /tmp/go${go_version}.linux-amd64.tar.gz -C /usr/local && \
  mkdir $GOPATH && \
  rm -rf /tmp/*

RUN go get github.com/onsi/ginkgo/ginkgo

# Install jq
RUN wget -O /usr/local/bin/jq 'https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64' && \
  chmod +x /usr/local/bin/jq

# Install bbl
RUN \
  wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v${bbl_version}/bbl-v${bbl_version}_linux_x86-64 -P /tmp && \
  mv /tmp/bbl-* /usr/local/bin/bbl && \
  cd /usr/local/bin && \
  chmod +x bbl

# Install the golang bosh CLI
RUN \
  wget https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64 --output-document="/usr/bin/bosh" && \
  chmod +x /usr/bin/bosh

# Install the cf CLI
RUN \
  wget -q -O cf.deb "https://cli.run.pivotal.io/stable?release=debian64&source=github-rel" && \
  dpkg -i cf.deb

# credhub-cli
RUN \
  wget https://github.com/cloudfoundry-incubator/credhub-cli/releases/download/${credhub_cli_version}/credhub-linux-${credhub_cli_version}.tgz -P /tmp && \
  tar xzvf /tmp/credhub-linux-${credhub_cli_version}.tgz -C /usr/local/bin && \
  chmod +x /usr/local/bin/credhub

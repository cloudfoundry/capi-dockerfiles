FROM golang:1.9-alpine

RUN apk --no-cache add \
    ca-certificates wget bash git make jq curl \
    python py-pip \
    iptables openssh-client \
    glide

RUN pip install sshuttle

WORKDIR /go

# Install CF CLI
RUN wget -O /tmp/cf.tgz 'https://cli.run.pivotal.io/stable?release=linux64-binary&version=6.32.0&source=github-rel' 2>&1 && \
  tar xf /tmp/cf.tgz cf && \
  mv ./cf /usr/local/bin/ && \
  rm /tmp/cf.tgz

# Install BOSH CLI
RUN wget -O /usr/local/bin/bosh 'https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.40-linux-amd64' 2>&1 && \
  chmod +x /usr/local/bin/bosh

RUN wget -O /usr/local/bin/dep 'https://github.com/golang/dep/releases/download/v0.3.2/dep-linux-amd64' 2>&1 && \
  chmod +x /usr/local/bin/dep

# Install bbl
RUN \
  wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v6.6.7/bbl-v6.6.7_linux_x86-64 -P /tmp && \
  mv /tmp/bbl-* /usr/local/bin/bbl && \
  cd /usr/local/bin && \
  chmod +x bbl

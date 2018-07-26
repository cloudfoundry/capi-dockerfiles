FROM ruby:2.4

RUN apt-get update && \
    apt-get -y install \
    build-essential \
    wget \
    xz-utils \
    lsof \
    jq \
    vim \
    netcat-openbsd \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -O /tmp/proxychains.tar.xz https://github.com/rofl0r/proxychains-ng/releases/download/v4.12/proxychains-ng-4.12.tar.xz && \
  mkdir /tmp/proxychains && \
  tar xf /tmp/proxychains.tar.xz -C /tmp/proxychains --strip-components=1 && \
  cd /tmp/proxychains && \
  ./configure --prefix=/usr --sysconfdir=/etc && \
  make install && \
  rm -rf /tmp/*

RUN \
  wget https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-5.0.1-linux-amd64 --output-document="/usr/bin/bosh" && \
  chmod +x /usr/bin/bosh

# Install bbl
RUN \
  wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v6.6.7/bbl-v6.6.7_linux_x86-64 -P /tmp && \
  mv /tmp/bbl-* /usr/local/bin/bbl && \
  cd /usr/local/bin && \
  chmod +x bbl

FROM ruby:2.3.4

RUN apt-get update && \
    apt-get -y install \
    build-essential \
    wget \
    xz-utils \
    lsof \
    jq \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -O /tmp/proxychains.tar.xz https://github.com/rofl0r/proxychains-ng/releases/download/v4.12/proxychains-ng-4.12.tar.xz && \
  mkdir /tmp/proxychains && \
  tar xf /tmp/proxychains.tar.xz -C /tmp/proxychains --strip-components=1 && \
  cd /tmp/proxychains && \
  ./configure --prefix=/usr --sysconfdir=/etc && \
  make install && \
  rm -rf /tmp/*

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.16-linux-amd64 && \
    chmod +x /usr/local/bin/bosh

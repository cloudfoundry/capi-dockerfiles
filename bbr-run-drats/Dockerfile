FROM cloudfoundrylondon/backup-and-restore-minimal

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

WORKDIR /go

# Install CF CLI
RUN wget -O /tmp/cf.tgz 'https://cli.run.pivotal.io/stable?release=linux64-binary&version=6.32.0&source=github-rel' 2>&1 && \
  tar xf /tmp/cf.tgz cf && \
  mv ./cf /usr/local/bin/ && \
  rm /tmp/cf.tgz

# Install bbl
RUN \
  wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v6.6.7/bbl-v6.6.7_linux_x86-64 -P /tmp && \
  mv /tmp/bbl-* /usr/local/bin/bbl && \
  cd /usr/local/bin && \
  chmod +x bbl

RUN wget -O /tmp/proxychains.tar.xz https://github.com/rofl0r/proxychains-ng/releases/download/v4.12/proxychains-ng-4.12.tar.xz && \
  mkdir /tmp/proxychains && \
  tar xf /tmp/proxychains.tar.xz -C /tmp/proxychains --strip-components=1 && \
  cd /tmp/proxychains && \
  ./configure --prefix=/usr --sysconfdir=/etc && \
  make install && \
  rm -rf /tmp/*

FROM cloudfoundrylondon/backup-and-restore-minimal

ENV bbl_version 6.6.7

RUN wget -q -O - https://raw.githubusercontent.com/starkandwayne/homebrew-cf/master/public.key | apt-key add -  && \
    echo "deb http://apt.starkandwayne.com stable main" | tee /etc/apt/sources.list.d/starkandwayne.list  && \
    apt-get update

RUN apt-get update && \
    apt-get -y install \
    build-essential \
    wget \
    xz-utils \
    lsof \
    jq \
    vim \
    netcat-openbsd \
    credhub-cli \
    bosh-bootloader \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /go

RUN cp /usr/bin/bbl /usr/bin/bbl-what

RUN wget -q -O /usr/bin/bbl 'https://github.com/cloudfoundry/bosh-bootloader/releases/download/v${bbl_version}/bbl-v${bbl_version}_linux_x86-64' && \
    chmod +x /usr/bin/bbl

# Install CF CLI
RUN wget -O /tmp/cf.tgz 'https://cli.run.pivotal.io/stable?release=linux64-binary&source=github-rel' 2>&1 && \
  tar xf /tmp/cf.tgz cf && \
  mv ./cf /usr/local/bin/ && \
  rm /tmp/cf.tgz

# Symlink BBR bosh-cli to bosh
RUN ln -s /usr/bin/bosh-cli /usr/local/bin/bosh

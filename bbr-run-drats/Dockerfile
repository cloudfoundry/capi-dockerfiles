FROM pcfplatformrecovery/backup-and-restore-minimal

ENV BBL_CLI_ARCH linux
ENV CREDHUB_CLI_ARCH linux

# Install CF CLI
RUN wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | apt-key add - && \
    echo "deb https://packages.cloudfoundry.org/debian stable main" | tee /etc/apt/sources.list.d/cloudfoundry-cli.list && \
    apt-get update

RUN apt-get -y remove cf7-cli

RUN apt-get update && \
    apt-get -y install \
    build-essential \
    wget \
    xz-utils \
    lsof \
    jq \
    vim \
    netcat-openbsd \
    cf8-cli \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /go

RUN BBL_LATEST=$(curl -s https://api.github.com/repos/cloudfoundry/bosh-bootloader/releases/latest  | \
    jq -r ".assets[] | select(.name | test(\"${BBL_CLI_ARCH}\")) | .browser_download_url") && \
    wget -q -O /usr/bin/bbl $BBL_LATEST && \
    chmod +x /usr/bin/bbl

RUN CREDHUB_LATEST=$(curl -s https://api.github.com/repos/cloudfoundry/credhub-cli/releases/latest  | \
    jq -r ".assets[] | select(.name | test(\"${CREDHUB_CLI_ARCH}\")) | .browser_download_url") && \
    wget -q -O /tmp/credhub.tar.gz $CREDHUB_LATEST && tar xzf /tmp/credhub.tar.gz -C /usr/bin/ ./credhub && \
    chmod +x /usr/bin/credhub

# Symlink BBR bosh-cli to bosh
RUN ln -s /usr/bin/bosh-cli /usr/local/bin/bosh

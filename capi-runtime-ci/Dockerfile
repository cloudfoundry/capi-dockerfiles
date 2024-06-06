FROM ruby:3.2-buster

ENV bosh_cli_version 7.6.1

ENV HOME /root
RUN \
  echo '' > $HOME/.bashrc && \
  echo "[ -f ~/.bashrc ] && source ~/.bashrc" >> $HOME/.bash_profile

RUN \
  apt-get update && \
  apt-get -y install \
    build-essential \
    curl \
    debconf-utils \
    git \
    libcurl4-openssl-dev \
    libpq-dev \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    software-properties-common \
    unzip \
    wget \
    zip \
    zlib1g-dev

RUN wget -O /usr/local/bin/bosh https://storage.googleapis.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64
RUN chmod +x /usr/local/bin/bosh

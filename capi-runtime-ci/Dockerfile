FROM ubuntu:trusty

ENV bosh_cli_version 6.4.1

ENV HOME /root
RUN \
  echo '' > $HOME/.bashrc && \
  echo "[ -f ~/.bashrc ] && source ~/.bashrc" >> $HOME/.bash_profile

RUN \
  echo "deb http://archive.ubuntu.com/ubuntu trusty-backports main restricted universe multiverse" > /etc/apt/sources.list.d/backports.list && \
  apt-get update && \
  apt-get -y install \
    bison \
    build-essential \
    curl \
    debconf-utils \
    jq/trusty-backports \
    libcurl4-openssl-dev \
    libmysqlclient-dev \
    libpq-dev \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    mercurial \
    python-software-properties \
    software-properties-common \
    python-pip \
    unzip \
    wget \
    zip \
    zlib1g-dev

RUN \
  add-apt-repository ppa:git-core/ppa -y && \
  apt-get update && \
  apt-get install -y git && \
  apt-get remove -y --purge software-properties-common

RUN \
  wget https://github.com/postmodern/ruby-install/archive/v0.4.1.tar.gz -P /tmp && \
  tar zxf /tmp/v0.4.1.tar.gz -C /tmp && \
  cd /tmp/ruby-install-0.4.1 && make install && \
  ruby-install ruby 2.7.2 && \
  rm -rf /usr/local/src/ruby-2.7.2 && \
  rm -rf /tmp/*

RUN \
  git clone https://github.com/postmodern/chruby /tmp/chruby && \
  cd /tmp/chruby && git reset --hard 310bd34d1fcbb3365814c85018114123cef5a41f && \
  cd /tmp/chruby && ./scripts/setup.sh && \
  echo 'source /usr/local/share/chruby/chruby.sh' >> $HOME/.bashrc && \
  echo 'chruby 2.7.2' >> $HOME/.bashrc && \
  rm -rf /tmp/*

RUN \
  bash -l -c "gem update --system" && \
  bash -l -c "gem install bundler -v 2.2.4 --no-document --force"

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64
RUN chmod +x /usr/local/bin/bosh

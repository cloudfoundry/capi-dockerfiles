FROM ruby:2.4
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN gem install bundler

RUN set -ex \
    && echo 'mysql-server mysql-server/root_password password password' | debconf-set-selections \
    && echo 'mysql-server mysql-server/root_password_again password password' | debconf-set-selections \
    && apt-get update \
    && apt-get -y install \
           mysql-server \
           postgresql-contrib \
           postgresql \
           apt-transport-https \
           software-properties-common \
    && apt-get clean \
    && chmod 755 /var/lib/mysql \
    && sed -i 's/peer/trust/' "$(find /etc/postgresql -name pg_hba.conf)" \
    && sed -i 's/md5/trust/' "$(find /etc/postgresql -name pg_hba.conf)" \
    && service mysql restart \
    && service postgresql restart \
    && echo 'CREATE DATABASE cc_test;' | mysql -u root -ppassword \
    && createdb -U postgres cc_test \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install MS SQL CLI
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
  apt-get install nodejs && \
  npm install -g sql-cli

# Install docker in order to run nested MS SQL docker image
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
  apt-key fingerprint 0EBFCD88 && \
  add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/debian \
     $(lsb_release -cs) \
     stable" && \
  apt-get update && \
  apt-get -y install docker-ce && \
  apt-get clean

ENV GOPATH $HOME/go
ENV PATH $HOME/go/bin:/usr/local/go/bin:$PATH
RUN \
  wget https://storage.googleapis.com/golang/go1.6.2.linux-amd64.tar.gz -P /tmp && \
  tar xzvf /tmp/go1.6.2.linux-amd64.tar.gz -C /usr/local && \
  mkdir $GOPATH && \
  rm -rf /tmp/*

RUN set -ex \
    && apt-get update \
    && apt-get -y install \
        vim \
        unzip \
        zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
    && wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/master/Gemfile.lock \
    && wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/master/Gemfile \
    && bundle install \
    && rm Gemfile \
    && rm Gemfile.lock \
    && rm -rf /tmp/* /var/tmp/*

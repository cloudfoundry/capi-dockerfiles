FROM ruby:2.7-buster
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN set -ex \
    && echo 'mysql-server mysql-server/root_password password password' | debconf-set-selections \
    && echo 'mysql-server mysql-server/root_password_again password password' | debconf-set-selections \
    # add old stretch repo until we can figure out how to get ccng to work with mariadb > 10.1
    && echo 'deb http://deb.debian.org/debian stretch main' | tee -a /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y install \
           default-mysql-server=1.0.2 \
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

ENV GOPATH $HOME/go
ENV PATH $HOME/go/bin:/usr/local/go/bin:$PATH
RUN \
  wget https://storage.googleapis.com/golang/go1.18.1.linux-amd64.tar.gz -P /tmp && \
  tar xzvf /tmp/go1.18.1.linux-amd64.tar.gz -C /usr/local && \
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
    && wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/main/Gemfile.lock \
    && wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/main/Gemfile \
    && bundle install \
    && rm Gemfile \
    && rm Gemfile.lock \
    && rm -rf /tmp/* /var/tmp/*

# Install protobuf
RUN set -ex \
    && wget https://github.com/protocolbuffers/protobuf/releases/download/v3.6.1/protoc-3.6.1-linux-x86_64.zip -O protoc.zip \
    && unzip -o protoc.zip \
    && mv include/google /usr/local/include \
    && mv bin/protoc /usr/local/bin \
    && rm -f protoc.zip

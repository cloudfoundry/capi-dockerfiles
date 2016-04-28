FROM ruby:2.3
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

# Bundler 1.12.x fixes an incompatibility with RubyGems 2.6.2+
# https://github.com/bundler/bundler/issues/4381
# We can remove this once bundler 1.12.x is released and baked into the
# ruby:2.3 docker image.
RUN gem install bundler -v 1.12.0.rc.4

RUN  \
    echo 'mysql-server mysql-server/root_password password password' | debconf-set-selections && \
    echo 'mysql-server mysql-server/root_password_again password password' | debconf-set-selections && \
    apt-get update && \
    apt-get -y install \
        mysql-server \
        postgresql-contrib \
        postgresql && \
    apt-get clean && \
    chmod 755 /var/lib/mysql && \
    sed -i 's/peer/trust/' "$(find /etc/postgresql -name pg_hba.conf)" && \
    sed -i 's/md5/trust/' "$(find /etc/postgresql -name pg_hba.conf)" && \
    service mysql restart && \
    service postgresql restart && \
    echo 'CREATE DATABASE cc_test;' | mysql -u root -ppassword && \
    createdb -U postgres cc_test

RUN  \
    apt-get update && \
    apt-get -y install \
        vim \
        unzip \
        zip && \
    apt-get clean

RUN \
    wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/master/Gemfile.lock && \
    wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/master/Gemfile && \
    bundle install && \
    rm Gemfile && \
    rm Gemfile.lock


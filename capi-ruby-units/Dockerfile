FROM ruby:3.2-bookworm
LABEL org.opencontainers.image.authors="CF CAPI team"
LABEL org.opencontainers.image.url="https://github.com/cloudfoundry/capi-dockerfiles"

RUN apt-get update && \
    apt-get -y install \
      lsb-release \
      lsof \
      zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q https://dev.mysql.com/get/mysql-apt-config_0.8.33-1_all.deb && \
    export DEBIAN_FRONTEND=noninteractive && \
    echo 'mysql-apt-config mysql-apt-config/select-preview select ' | debconf-set-selections && \
    echo 'mysql-apt-config mysql-apt-config/select-product select Ok' | debconf-set-selections && \
    echo 'mysql-apt-config mysql-apt-config/select-server select mysql-8.0' | debconf-set-selections && \
    echo 'mysql-apt-config mysql-apt-config/select-tools select ' | debconf-set-selections && \
    dpkg -i  ./mysql-apt-config_0.8.33-1_all.deb && \
    apt-get update && \
    apt-get install -y mysql-server && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* mysql-apt-config_*.deb && \
    unset DEBIAN_FRONTEND

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg && \
    apt-get update && \
    apt-get -y install postgresql-16 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./mysql /etc/init.d/mysql
RUN chmod a+x /etc/init.d/mysql && \
    service mysql start && \
    mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';" && \
    sed -i 's/peer$/trust/;s/scram-sha-256/trust/' /etc/postgresql/16/main/pg_hba.conf && \
    service postgresql restart

RUN wget -q https://raw.githubusercontent.com/cloudfoundry/capi-release/develop/spec/Gemfile.lock && \
    wget -q https://raw.githubusercontent.com/cloudfoundry/capi-release/develop/spec/Gemfile && \
    bundle config set --local without 'development' && \
    bundle install && \
    rm Gemfile && \
    rm Gemfile.lock && \
    rm -rf /tmp/* /var/tmp/*

RUN wget -q https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/main/Gemfile.lock && \
    wget -q https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/main/Gemfile && \
    bundle config set --local without 'development' && \
    bundle install && \
    rm Gemfile && \
    rm Gemfile.lock && \
    rm -rf /tmp/* /var/tmp/*

FROM ruby:3.2-bookworm
LABEL org.opencontainers.image.authors="CF CAPI team"
LABEL org.opencontainers.image.url="https://github.com/cloudfoundry/capi-dockerfiles"

RUN apt-get update && \
    apt-get -y install \
      default-mysql-server \
      lsb-release \
      zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg && \
    apt-get update && \
    apt-get -y install postgresql-16 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN ln -s /etc/init.d/mariadb /etc/init.d/mysql && \
    service mysql restart && \
    mysql -e "SET PASSWORD FOR 'root'@'localhost' = PASSWORD('password');" && \
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

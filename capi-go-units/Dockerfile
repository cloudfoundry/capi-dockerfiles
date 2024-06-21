FROM golang
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN apt-get update && \
    apt-get -y install \
      unzip \
      lsb-release && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg && \
    apt-get update && \
    apt-get -y install postgresql-12 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    sed -i 's/peer$/trust/;s/md5$/trust/' /etc/postgresql/12/main/pg_hba.conf

RUN service postgresql start && \
    createdb -U postgres locket && \
    psql -h localhost -Upostgres -c "CREATE USER locket WITH createrole superuser password 'locket_pw';"

FROM golang
LABEL org.opencontainers.image.authors="CF CAPI team"
LABEL org.opencontainers.image.url="https://github.com/cloudfoundry/capi-dockerfiles"

RUN apt-get update && \
    apt-get -y install lsb-release && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg && \
    apt-get update && \
    apt-get -y install postgresql-16 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN sed -i 's/peer$/trust/;s/scram-sha-256/trust/' /etc/postgresql/16/main/pg_hba.conf && \
    service postgresql restart && \
    createdb -U postgres locket && \
    psql -h localhost -U postgres -c "CREATE USER locket WITH createrole superuser password 'locket_pw';"

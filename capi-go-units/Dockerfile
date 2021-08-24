FROM golang
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN set -ex \
    && apt-get update \
    && apt-get -y install \
        unzip \
        lsb-release \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
  apt-get update && \
  apt-get -y install postgresql-9.4 && \
  apt-get clean && \
  sed -i 's/peer/trust/' /etc/postgresql/9.4/main/pg_hba.conf && \
  sed -i 's/md5/trust/' /etc/postgresql/9.4/main/pg_hba.conf

RUN service postgresql start && \
  createdb -U postgres locket && \
  psql -h localhost -Upostgres -c "CREATE USER locket WITH createrole superuser password 'locket_pw';"

# kubebuilder for capi-k8s-release controllers
RUN curl -L https://github.com/kubernetes-sigs/kubebuilder/releases/download/v2.3.1/kubebuilder_2.3.1_linux_amd64.tar.gz | tar -xz -C /tmp/ && \
    mv /tmp/kubebuilder_2.3.1_linux_amd64 /usr/local/kubebuilder

ENV PATH $PATH:/usr/local/kubebuilder/bin

FROM relintdockerhubpushbot/cf-deployment-concourse-tasks:v2.2.0
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles
# The FROM should match the repo and tag in this file:
#   https://github.com/cloudfoundry/cf-deployment-concourse-tasks/blob/master/bbl-up/task.yml

RUN \
  apt-get -y install \
    mercurial \
    apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV GOPATH $HOME/go
ENV PATH $HOME/go/bin:/usr/local/go/bin:$PATH
RUN \
  wget https://storage.googleapis.com/golang/go1.6.2.linux-amd64.tar.gz -P /tmp && \
  tar xzvf /tmp/go1.6.2.linux-amd64.tar.gz -C /usr/local && \
  mkdir $GOPATH && \
  rm -rf /tmp/*

RUN go get github.com/square/certstrap

RUN echo "deb https://packages.cloud.google.com/apt cloud-sdk-$(lsb_release -c -s) main" >> \
  /etc/apt/sources.list.d/google-cloud-sdk.list && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
  apt-get update && \
  apt-get -y install google-cloud-sdk && \
  apt-get clean

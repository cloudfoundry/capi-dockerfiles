FROM cloudfoundry/cf-deployment-concourse-tasks:v15.0.0
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN \
  apt-get update && \
  apt-get -y install \
    mercurial \
    python3-pip \
    apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip3 install yq
RUN wget https://github.com/square/certstrap/releases/download/v1.2.0/certstrap-1.2.0-linux-amd64 && \
  mv certstrap-1.2.0-linux-amd64 /go/bin/certstrap && \
  chmod u+x /go/bin/certstrap

RUN echo "deb https://packages.cloud.google.com/apt cloud-sdk-$(lsb_release -c -s) main" >> \
  /etc/apt/sources.list.d/google-cloud-sdk.list && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
  apt-get update && \
  apt-get -y install google-cloud-sdk && \
  apt-get clean

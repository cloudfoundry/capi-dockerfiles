FROM cloudfoundry/cf-deployment-concourse-tasks
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

RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.asc] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | tee /usr/share/keyrings/cloud.google.asc && \
  apt-get update && \
  apt-get -y install google-cloud-cli && \
  apt-get clean

# https://kubernetes.io/docs/tasks/tools/install-kubectl/
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \ 
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list && \
  apt-get update && \
  apt-get install -y kubectl

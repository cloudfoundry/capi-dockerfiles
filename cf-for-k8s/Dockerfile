FROM google/cloud-sdk:278.0.0-alpine

RUN curl -sSL https://sdk.cloud.google.com | bash

RUN curl -sSLO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

ENV PATH $PATH:/usr/local/go/bin:/root/go/bin
RUN wget https://dl.google.com/go/go1.13.7.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.13.7.linux-amd64.tar.gz && \
    rm -rf go1.13.7.linux-amd64.tar.gz && \
    GO111MODULE="on" go get -v github.com/onsi/gomega/... && \
    GO111MODULE="on" go install -v github.com/onsi/ginkgo/ginkgo

RUN apk add --no-cache openssl && \
    curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

RUN apk add --no-cache perl-utils && \
    wget -O- https://k14s.io/install.sh | bash

RUN apk add --no-cache jq=1.6-r0

RUN apk add --no-cache python3 && \
    pip3 install yq

RUN apk add --no-cache gcc && \
    apk add --no-cache libc-dev

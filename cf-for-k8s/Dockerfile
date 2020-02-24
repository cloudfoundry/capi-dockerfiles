FROM relintdockerhubpushbot/cf-test-runner

RUN apt install git bash curl python3 openssl perl-utils bind-tools jq=1.6-r0

RUN curl -sSL https://sdk.cloud.google.com | bash

RUN curl -sSLO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

RUN curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

RUN wget -O- https://k14s.io/install.sh | bash

RUN pip3 install yq

# https://github.com/golang/go/issues/28065
ENV CGO_ENABLED=0
ENV PATH $PATH:/root/google-cloud-sdk/bin

ENV bosh_cli_version 6.2.1
RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64
RUN chmod +x /usr/local/bin/bosh

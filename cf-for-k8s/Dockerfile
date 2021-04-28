FROM relintdockerhubpushbot/cf-test-runner


RUN apt-get update && \
    apt install -y git bash curl python3 python3-pip openssl dnsutils jq gnupg gnupg1 gnupg2

RUN rm -f /usr/local/bin/cf
RUN wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key |\
        apt-key add - && \
    echo "deb https://packages.cloudfoundry.org/debian stable main" |\
        tee /etc/apt/sources.list.d/cloudfoundry-cli.list

RUN apt-get update &&\
    apt-get install cf7-cli &&\
    apt-get clean

RUN ln -sf $(which cf7) /usr/local/bin/cf

RUN curl -sSL https://sdk.cloud.google.com | bash

RUN curl -sSLO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

RUN curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

RUN wget -O- https://k14s.io/install.sh | bash

# https://github.com/golang/go/issues/28065
ENV CGO_ENABLED=0
ENV PATH $PATH:/root/google-cloud-sdk/bin

RUN pip3 install yq

ENV bosh_cli_version 6.4.2
RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64
RUN chmod +x /usr/local/bin/bosh

RUN cf install-plugin -f -r CF-Community "log-cache"

ENV VELERO_VERSION v1.5.2
RUN \
  wget https://github.com/vmware-tanzu/velero/releases/download/${VELERO_VERSION}/velero-${VELERO_VERSION}-linux-amd64.tar.gz -P /tmp && \
  tar xzvf /tmp/velero-${VELERO_VERSION}-linux-amd64.tar.gz -C /tmp/ && \
  mv /tmp/velero-${VELERO_VERSION}-linux-amd64/velero /usr/local/bin/velero && \
  chmod +x /usr/local/bin/velero && \
  rm -rf /tmp/velero*

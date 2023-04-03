FROM ubuntu:latest

ENV bosh_cli_version 7.2.2

RUN apt-get update && \
    apt-get -y install \
    ca-certificates wget bash tar util-linux \
    python3 \
    git \
    build-essential \
    # needed to render bosh templates
    ruby ruby-dev
    # needed to run Google CPI packaging scripts


RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-${bosh_cli_version}-linux-amd64
RUN chmod +x /usr/local/bin/bosh

# Every once in a while, you'll see "Updates are available for some Cloud SDK components."
# You can find the latest downloads at https://cloud.google.com/sdk/downloads
RUN wget -O /tmp/google-sdk.zip https://dl.google.com/dl/cloudsdk/channels/rapid/google-cloud-sdk.zip && \
  unzip /tmp/google-sdk.zip -d $HOME && \
  rm /tmp/google-sdk.zip

RUN $HOME/google-cloud-sdk/install.sh \
      --usage-reporting=false \
      --additional-components gsutil

RUN ln -s $HOME/google-cloud-sdk/bin/gcloud /usr/local/bin/
RUN ln -s $HOME/google-cloud-sdk/bin/gsutil /usr/local/bin/

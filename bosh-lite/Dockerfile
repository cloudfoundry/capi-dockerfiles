FROM alpine:latest

ENV bosh_cli_version 6.1.0

RUN apk update && \
    apk --no-cache add \
    ca-certificates wget bash tar util-linux \
    python \
    # needed to render bosh templates
    ruby ruby-dev \
    # needed to run Google CPI packaging scripts
    make alpine-sdk

# the Google CPI Go blob is dynamically linked against glibc
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
  wget -q -O /tmp/glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk && \
  apk add /tmp/glibc.apk && \
  rm -rf /tmp/glibc.apk

RUN gem install json --no-rdoc --no-ri # json is not a default gem in alpine

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

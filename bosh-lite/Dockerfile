FROM alpine:latest

RUN apk update && \
    apk --no-cache add \
    ca-certificates wget bash tar util-linux \
    python \
    # needed to render bosh templates
    ruby ruby-dev \
    # needed to run Google CPI packaging scripts
    make alpine-sdk

# the Google CPI Go blob is dynamically linked against glibc
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub && \
  wget -q -O /tmp/glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk && \
  apk add /tmp/glibc.apk && \
  rm -rf /tmp/glibc.apk

RUN gem install json --no-rdoc --no-ri # json is not a default gem in alpine

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.1-linux-amd64
RUN chmod +x /usr/local/bin/bosh

RUN wget -O /tmp/google-sdk.tgz https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-152.0.0-linux-x86_64.tar.gz && \
  tar xvf /tmp/google-sdk.tgz -C $HOME && \
  rm /tmp/google-sdk.tgz

RUN ln -s $HOME/google-cloud-sdk/bin/gcloud /usr/local/bin/
RUN ln -s $HOME/google-cloud-sdk/bin/gsutil /usr/local/bin/

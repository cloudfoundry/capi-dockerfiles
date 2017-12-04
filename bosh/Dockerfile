FROM alpine:3.6

RUN apk update && \
    apk --no-cache add \
    ca-certificates wget bash tar \
    gcc alpine-sdk jq \
    ruby ruby-dev make && \
    rm -rf /var/cache/apk/*

RUN gem install json --no-rdoc --no-ri # json is not a default gem in alpine

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.30-linux-amd64
RUN chmod +x /usr/local/bin/bosh

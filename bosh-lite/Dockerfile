FROM alpine:latest

RUN apk update && \
    apk --no-cache add \
    ca-certificates wget bash \
    python \
    py-pip

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.1-linux-amd64
RUN chmod +x /usr/local/bin/bosh

RUN pip install awscli

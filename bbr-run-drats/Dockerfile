FROM golang:1.9-alpine

RUN apk --no-cache add \
    ca-certificates wget bash git make \
    python py-pip \
    iptables openssh-client \
    glide

RUN pip install sshuttle

WORKDIR /go

# Install bbr from source as release binaries don't run on alpine
# https://github.com/cloudfoundry-incubator/bosh-backup-and-restore/issues/6
RUN mkdir -p src/github.com/cloudfoundry-incubator/ && \
  cd src/github.com/cloudfoundry-incubator/ && \
  git clone https://github.com/cloudfoundry-incubator/bosh-backup-and-restore.git && \
  cd bosh-backup-and-restore && \
  git checkout v1.1.0 && \
  make setup && \
  CGO_ENABLED=0 go build -o /usr/local/bin/bbr ./cmd/bbr/ && \
  rm -rf src/github.com/cloudfoundry-incubator/bosh-backup-and-restore

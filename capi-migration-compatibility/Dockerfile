FROM ruby:2.3.4

RUN apt-get update && \
    apt-get -y install \
    build-essential \
    wget \
    unzip \
    tsocks \
    lsof \
    jq \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Socks Proxy tunnels should be opened on port 8080
RUN printf 'server = 127.0.0.1\n\
server_type = 5\n\
server_port = 8080\n'\
> /etc/tsocks.conf

RUN wget -O /usr/local/bin/bosh https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-2.0.16-linux-amd64 && \
    chmod +x /usr/local/bin/bosh

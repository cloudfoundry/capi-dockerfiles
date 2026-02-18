FROM ruby:3.3-bookworm
LABEL org.opencontainers.image.authors="CF CAPI team"
LABEL org.opencontainers.image.url="https://github.com/cloudfoundry/capi-dockerfiles"

RUN apt-get update && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/main/docs/v3/Gemfile.lock && \
    wget -q https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/main/docs/v3/Gemfile && \
    bundle install && \
    rm Gemfile && \
    rm Gemfile.lock && \
    rm -rf /tmp/* /var/tmp/*

FROM cloudfoundry/capi:ruby-units
MAINTAINER https://github.com/cloudfoundry/capi-dockerfiles

RUN set -ex \
    && apt-get update \
    && apt-get -y install \
        git \
        libcurl4-openssl-dev \
        libssl-dev \
        python-dev \
        python3-dev \
        python-software-properties \
        software-properties-common \
        python-pip \
    && bash -l -c "pip install awscli" \
    && bash -l -c "pip install s3cmd" \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN set -ex \
    && wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/master/docs/v3/Gemfile.lock \
    && wget https://raw.githubusercontent.com/cloudfoundry/cloud_controller_ng/master/docs/v3/Gemfile \
    && bundle install \
    && rm Gemfile \
    && rm Gemfile.lock \
    && rm -rf /tmp/* /var/tmp/*

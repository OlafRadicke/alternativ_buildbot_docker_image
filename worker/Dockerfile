FROM        ubuntu:18.04
MAINTAINER  Olaf radicke

ARG         DEBIAN_FRONTEND=noninteractive

# Install security updates and required packages
RUN         apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install -q \
    build-essential \
    git \
    subversion \
    python3-dev \
    libffi-dev \
    libssl-dev \
    python3-setuptools \
    python3-pip \
    dumb-init \
    curl && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 --no-cache-dir install 'twisted[tls]' && \
    pip3 install virtualenv && \
    pip3 install buildbot-worker && \
    mkdir /buildbot && \
    useradd -ms /bin/bash buildbot

COPY buildbot.tac /buildbot/buildbot.tac

USER buildbot
WORKDIR /buildbot

CMD ["/usr/bin/dumb-init", "twistd", "--pidfile=", "-ny", "buildbot.tac"]

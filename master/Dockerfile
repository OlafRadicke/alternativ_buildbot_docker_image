FROM        alpine:3.11
MAINTAINER  Olaf Radicke
# Based on "Installation From PyPI" under http://docs.buildbot.net/latest/manual/installation/installation.html#installation-from-pypi
# Clean and strait forward

COPY ./srv_buildbot /srv/buildbot
RUN apk add --no-cache \
        git \
        py3-pip \
        curl \
        python3 \
        dumb-init \
        python3-dev \
        gcc \
        musl-dev \
        libffi-dev \
        libressl-dev \
        postgresql-dev 
        # alpine-sdk \
        # tar \
        # tzdata \
        # openssh
        # postgresql-libs \

RUN pip3 install --upgrade pip
RUN pip3 install buildbot==2.7.0
RUN pip3 install buildbot-www
RUN pip3 install buildbot-waterfall-view
RUN pip3 install buildbot-console-view
RUN pip3 install psycopg2-binary
# RUN pip install buildbot-worker
RUN adduser buildbot --disabled-password
RUN chown buildbot.buildbot /srv/buildbot

USER buildbot
WORKDIR /srv/buildbot
RUN ls -lah

CMD ["dumb-init", "/srv/buildbot/start_buildbot.sh"]

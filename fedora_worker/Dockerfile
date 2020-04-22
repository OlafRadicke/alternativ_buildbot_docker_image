
FROM        fedora:31
MAINTAINER  Olaf radicke

RUN echo "buildbot	ALL=(ALL)	NOPASSWD: ALL" >> /etc/sudoers

RUN dnf install -y dnf-plugins-core \
    rpm-build \
    redhat-rpm-config \
    rpmdevtools \
    gcc \
    e2fsprogs-devel \
    glib2-devel  \
    gpm-devel \
    libssh2-devel \
    perl-generators \
    slang-devel \
    make \
    git \
    python3-devel \
    libffi-devel \
    openssl-devel \
    python3-setuptools \
    python3-pip \
    dumb-init \
    curl 
    
RUN pip3 --no-cache-dir install 'twisted[tls]' && \
    pip3 install virtualenv && \
    pip3 install buildbot-worker && \
    mkdir /buildbot && \
    useradd -ms /bin/bash buildbot


COPY buildbot.tac /buildbot/buildbot.tac

# USER buildbot
WORKDIR /buildbot
USER buildbot

CMD ["/usr/bin/dumb-init", "twistd", "--pidfile=", "-ny", "buildbot.tac"]

FROM alpine:3.11

RUN echo -e "https://nl.alpinelinux.org/alpine/v3.11/main\nhttps://nl.alpinelinux.org/alpine/v3.11/community" > /etc/apk/repositories
COPY pip/pip.conf pip.conf
COPY requirements.txt .
ENV PIP_CONFIG_FILE pip.conf
RUN apk --no-cache add \
        sudo \
        tar \
	    unzip \
	    gettext \
	    nano \
	    bash \
        python3\
        py3-pip \
        openssl \
        ca-certificates \
        sshpass \
        openssh-client \
        rsync \
        git && \
    apk --no-cache add --virtual build-dependencies \
        python3-dev \
        libffi-dev \
        openssl-dev \
        build-base && \
    pip3 install --default-timeout=100 --upgrade pip && \
    pip3 install -r requirements.txt && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/* && \
    rm -rf /root/.cache && \
    rm -rf pip.conf && \
    rm -rf requirements.txt

RUN mkdir /ansible && \
    mkdir -p /etc/ansible && \
    echo 'localhost' > /etc/ansible/hosts && \
    chown -R 1000:1000 /ansible

WORKDIR /ansible

RUN adduser ansible -u 1000 -D

USER 1000:1000

CMD [ "ansible-playbook", "--version" ]

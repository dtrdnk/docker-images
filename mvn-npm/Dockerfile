FROM ubuntu:20.04

ARG UID=1000
ARG GID=1000
ARG USER=maven
ARG HOME=/home/maven

RUN groupadd -g ${GID} ${USER} || groupmod -n ${USER} `getent group ${GID} | cut -d: -f1` \
    && useradd --shell /bin/bash -u ${UID} -g ${GID} -m ${USER} \
    && apt-get -qq update \
    && apt-get -qq -y --no-install-recommends install \
    curl \
    git \
    openjdk-11-jdk \
    maven

RUN curl -sL https://deb.nodesource.com/setup_19.x | bash - \
  && apt-get -qq -y --no-install-recommends install nodejs \
  && rm -rf /var/lib/apt/lists/* \

# workaround for workdir and non-root user
RUN mkdir ${HOME}/.m2
WORKDIR ${HOME}
USER ${USER}

CMD ["/bin/bash"]
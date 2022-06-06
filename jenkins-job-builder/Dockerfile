FROM python:3.8.13

RUN useradd jenkins -m -u 1000 -s /bin/bash

RUN  mkdir /.cache && chmod 700 /.cache \
    && chown -R 1000:1000 /.cache \
    && chown -R 1000:1000 /opt \
    && chown -R 1000:1000 /usr/local/lib \
    && chown -R 1000:1000 /usr/local/bin

USER 1000:1000

WORKDIR /opt

RUN cd /opt \
	&& git clone -b 4.1.0 --single-branch https://opendev.org/jjb/jenkins-job-builder.git \
	&& cd /opt/jenkins-job-builder \
	&& pip install -r requirements.txt \
	&& python setup.py install \
	&& rm -R /opt/jenkins-job-builder

CMD ["jenkins-job-builder", "--version"]

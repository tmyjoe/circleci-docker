FROM circleci/node:10

LABEL maintainer="Tomoya Honjo <tomoya.honjo22@gmail.com>"

RUN sudo apt-get install -y zip python python-dev python-pip
RUN sudo pip install --upgrade pip
RUN sudo pip install colorama==0.3.7 awscli awsebcli

ENV DOCKERVERSION=17.06.0-ce
ENV PATH /google-cloud-sdk/bin:$PATH

RUN mkdir /tmp/docker-build && cd /tmp/docker-build \
    && curl -L -o /tmp/docker-build/docker.tgz https://download.docker.com/linux/static/stable/x86_64/docker-17.03.0-ce.tgz \
    && sudo tar xzvf docker.tgz \
    && sudo mv docker /usr/local/bin \
    && rm -r /tmp/docker-build

USER root

RUN apt-get install lsb-release
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y && apt-get install google-cloud-sdk -y
RUN sudo apt-get install kubectl

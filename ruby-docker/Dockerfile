FROM circleci/ruby:2.5.1-node

LABEL maintainer="Tomoya Honjo <tomoya.honjo22@gmail.com>"

ENV DOCKERVERSION=17.06.0-ce
ENV PATH /google-cloud-sdk/bin:$PATH

RUN mkdir /tmp/docker-build && cd /tmp/docker-build \
    && curl -L -o /tmp/docker-build/docker.tgz https://download.docker.com/linux/static/stable/x86_64/docker-17.03.0-ce.tgz \
    && sudo tar xzvf docker.tgz \
    && sudo mv docker /usr/local/bin \ 
    && rm -r /tmp/docker-build 

RUN sudo apt-get install -y zip python python-pip
RUN sudo pip install awscli awsebcli
RUN curl https://sdk.cloud.google.com | bash
ENV PATH $PATH:~/google-cloud-sdk/bin:

FROM circleci/golang

LABEL maintainer="Tomoya Honjo <tomoya.honjo22@gmail.com>"

ENV DOCKERVERSION=17.06.0-ce

RUN mkdir /tmp/docker-build && cd /tmp/docker-build \
    && curl -L -o /tmp/docker-build/docker.tgz https://download.docker.com/linux/static/stable/x86_64/docker-17.03.0-ce.tgz \
    && sudo tar xzvf docker.tgz \
    && sudo mv docker /usr/local/bin \
    && rm -r /tmp/docker-build

RUN sudo apt-get install -y zip python python-dev python-pip
RUN sudo pip install --upgrade pip
RUN sudo pip install colorama==0.3.7 awscli awsebcli

USER root

RUN apt-get install lsb-release
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y && apt-get install google-cloud-sdk -y
RUN sudo apt-get install kubectl

RUN apt-get -y install mysql-client
RUN go get -u -d gocv.io/x/gocv
RUN cd $GOPATH/src/gocv.io/x/gocv && make install

# Note: Latest version of helm may be found at:
# https://github.com/kubernetes/helm/releases
ENV HELM_VERSION="v2.9.1"

RUN wget -q http://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > /usr/local/bin/helm \
    && chmod +x /usr/local/bin/helm

FROM circleci/terraform:0.11.7

LABEL maintainer="Tomoya Honjo <tomoya.honjo22@gmail.com>"

USER root

ENV CLOUD_SDK_VERSION 203.0.0

ENV PATH /google-cloud-sdk/bin:$PATH
RUN apk --no-cache add \
        curl \
        python \
        py-crcmod \
        bash \
        libc6-compat \
        openssh-client \
        git \
    && curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    tar xzf google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    rm google-cloud-sdk-${CLOUD_SDK_VERSION}-linux-x86_64.tar.gz && \
    ln -s /lib /lib64 && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud --version

RUN mkdir $HOME/.terraform.d && mkdir $HOME/.terraform.d/plugins
RUN wget https://github.com/akshaykarle/terraform-provider-mongodbatlas/releases/download/v0.6.1/terraform-provider-mongodbatlas_v0.6.1_linux_amd64 && \
    mv terraform-provider-mongodbatlas_v0.6.1_linux_amd64 $HOME/.terraform.d/plugins/terraform-provider-mongodbatlas_v0.6.1
RUN chmod +x $HOME/.terraform.d/plugins/terraform-provider-mongodbatlas_v0.6.1
RUN wget https://github.com/mcuadros/terraform-provider-helm/releases/download/v0.5.1/terraform-provider-helm_v0.5.1_linux_amd64.tar.gz && \
    tar -xvf terraform-provider-helm*.tar.gz && \
    mv terraform-provider-helm*/terraform-provider-helm $HOME/.terraform.d/plugins/
RUN chmod +x $HOME/.terraform.d/plugins/terraform-provider-helm
RUN file="$(ls -1 $HOME/.terraform.d/plugins)" && echo $file

RUN gcloud components update && gcloud components install beta

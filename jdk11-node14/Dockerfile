FROM debian:stable
LABEL maintainer="Tomasz Miller"

ENV TZ=Europe/Warsaw
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y --no-install-recommends  \
        software-properties-common \
        xvfb \
        ca-certificates \
        curl \
        file \
        fonts-dejavu-core \
        g++ \
        git \
        locales \
        java-common \
        maven \
        openssh-client \
        patch \
        uuid-runtime \
        unzip \
        zip \
        jq \
        python3 \
        make \
    && rm -rf /var/lib/apt/lists/*

# Installing Amazon Corretto 11 JDK
RUN curl -L -o "amazon-corretto-11-x64-linux-jdk.deb" https://corretto.aws/downloads/latest/amazon-corretto-11-x64-linux-jdk.deb
RUN dpkg --install amazon-corretto-11-x64-linux-jdk.deb

# Set Java environment
ENV JAVA_HOME=/usr/lib/jvm/java-11-amazon-corretto \
    PATH="/usr/lib/jvm/java-11-amazon-corretto/bin:$PATH"

# Set Maven environment
ENV MAVEN_HOME /usr/share/maven \
    MAVEN_CONFIG "$USER_HOME_DIR/.m2"

# Installing Node.js LTS (v14.x)
# https://github.com/nodesource/distributions/blob/master/README.md#debinstall
RUN curl -fsSL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get update
RUN apt-get install -y nodejs
RUN node -v

# Installing latest npm v7
RUN npm install -g npm@next-8
RUN npm -v

# Installing yarn
RUN npm install -g yarn
RUN yarn -v

# Installing TypeScript
RUN npm install -g typescript
RUN tsc -v

# Default to UTF-8 file.encoding
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    LANGUAGE=C.UTF-8

# Create Bitbucket pipelines dirs and users
USER root
RUN mkdir -p /opt/atlassian/bitbucketci/agent/build \
    && sed -i '/[ -z \"PS1\" ] && return/a\\ncase $- in\n*i*) ;;\n*) return;;\nesac' /root/.bashrc \
    && useradd -m -s /bin/bash pipelines

WORKDIR /home/pipelines

# Installing AWS-SAM-CLI
RUN curl -L -o "awssamcli.zip" "https://github.com/aws/aws-sam-cli/releases/download/v1.66.0/aws-sam-cli-linux-x86_64.zip" \
    && unzip -d awssamcli awssamcli.zip \
    && ./awssamcli/install
RUN sam --version

# Installing AWS-CLI
RUN curl -L -o "awscliv2.zip" "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" \
    && unzip awscliv2.zip \
    && ./aws/install
RUN aws --version

# Installing AWS CDK
RUN npm install -g aws-cdk
RUN cdk --version

USER pipelines

WORKDIR /opt/atlassian/bitbucketci/agent/build
ENTRYPOINT /bin/bash

RUN java -version
RUN mvn --version
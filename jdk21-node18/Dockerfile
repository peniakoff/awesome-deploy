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

# Installing Amazon Corretto 21 JDK
RUN curl -sSL https://apt.corretto.aws/corretto.key | gpg --dearmor -o /usr/share/keyrings/corretto-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/corretto-keyring.gpg] https://apt.corretto.aws stable main" | tee /etc/apt/sources.list.d/corretto.list
RUN apt-get update && apt-get install -y java-21-amazon-corretto-jdk

# Set Java environment
ENV JAVA_HOME=/usr/lib/jvm/java-21-amazon-corretto \
    PATH="/usr/lib/jvm/java-21-amazon-corretto/bin:$PATH"

# Set Maven environment
ENV MAVEN_HOME /usr/share/maven \
    MAVEN_CONFIG "$USER_HOME_DIR/.m2"

# Installing Node.js LTS (v18.x)
# https://github.com/nodesource/distributions/blob/master/README.md#debinstall
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get update \
    && apt-get install -y nodejs
RUN node -v
RUN npm -v

# Installing yarn
RUN npm install -g yarn
RUN yarn -v

# Installing TypeScript
RUN npm install -g typescript
RUN tsc -v

# Installing pnpm
RUN npm install -g pnpm
RUN pnpm -v

# Default to UTF-8 file.encoding
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    LANGUAGE=C.UTF-8

# Create Bitbucket pipelines dirs and users
USER root
RUN mkdir -p /opt/atlassian/bitbucketci/agent/build \
    && sed -i '/[ -z \"PS1\" ] && return/a\\ncase $- in\n*i*) ;;\n*) return;;\nesac' /root/.bashrc \
    && useradd -m -s /bin/bash pipelines
RUN git --version
RUN git config --system --add safe.directory '*'

WORKDIR /home/pipelines

# Installing AWS-SAM-CLI
RUN curl -L -o "awssamcli.zip" "https://github.com/aws/aws-sam-cli/releases/download/v1.121.0/aws-sam-cli-linux-x86_64.zip"
RUN unzip -d awssamcli awssamcli.zip
RUN ./awssamcli/install
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

# Check versions
RUN java -version
RUN mvn --version
RUN node -v
RUN npm -v
RUN yarn -v
RUN tsc -v
RUN sam --version
RUN aws --version
RUN cdk --version
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
        openssh-client \
        patch \
        uuid-runtime \
        unzip \
        zip \
        jq \
        python3 \
        make \
    && rm -rf /var/lib/apt/lists/*

# Installing nvm
SHELL ["/bin/bash", "--login", "-c"]
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
RUN nvm -v

# Installing Node.js (latest v14)
RUN nvm install 14
RUN node -v
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
RUN git --version
RUN git config --system --add safe.directory '*'

WORKDIR /home/pipelines

# Installing AWS-SAM-CLI
RUN curl -L -o "awssamcli.zip" "https://github.com/aws/aws-sam-cli/releases/download/v1.94.0/aws-sam-cli-linux-x86_64.zip" \
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

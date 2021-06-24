# AWeSome-deploy
Docker linux image for deployment (eg. via Bitbucket's Pipelines) to AWS

Depends on the branch (and tag) this image contains different tools for deploying your stuff to AWS.
Core for Dockerimage based on the `debian:stable` image and by default contains OpenJDK 11, Maven and Python 3, Make, AWS SAM CLI and AWS CLI (latest version for default image is `v1.1.0`).

Default Linux timezone is set to Europe/Warsaw and file encoding is set to UTF-8.

If you need also NodeJS and npm or/and yarn, you should use image from `node` branch (latest version is `v1.1.0-node`).

If you need JDK8 (Amazon Corretto), you should use image from `jdk8` branch (latest version is `v1.1.0-jdk8`).
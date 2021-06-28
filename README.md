# AWeSome-deploy
Docker linux image for deployment (eg. via Bitbucket's Pipelines) to AWS

Depends on the branch (and tag) this image contains different tools for deploying your stuff to AWS.
Core for Dockerimage based on the `debian:stable` image and by default contains Amazon Corretto 11 JDK, Maven, Python 3, Make, AWS SAM CLI and AWS CLI (latest version for default image is `peniakoff/awesome-deploy:jdk11-latest`).

Default Linux timezone is set to Europe/Warsaw and file encoding is set to UTF-8.

If you need also NodeJS and npm or/and yarn, you should use image `peniakoff/awesome-deploy:jdk11-node14-latest`.

If you need Amazon Corretto 8 JDK, you should use image `peniakoff/awesome-deploy:jdk8-latest`.

If you need Amazon Corretto 8 JDK and NodeJS, you should use image `peniakoff/awesome-deploy:jdk8-node14-latest`.

If you need more features/tools provided in the images, just open new discuss here https://github.com/peniakoff/awesome-deploy/discussions.
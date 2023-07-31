# AWeSome-deploy
Docker linux image for deployment (eg. via Bitbucket's Pipelines) to AWS

Depends on the tag image contains different tools for deploying your stuff to AWS.
Core for Dockerimage based on the `debian:stable` image and by default contains Amazon Corretto 11 JDK, Maven, Python 3, Make, AWS SAM CLI (`v1.94.0`) and AWS CLI.

Default Linux timezone is set to Europe/Warsaw and file encoding is set to UTF-8.

Images with NodeJS support also AWS CDK tool.

Latest version for default image with JDK 11 is `peniakoff/awesome-deploy:jdk11-latest`.

If you need also NodeJS with npm and yarn, you should use image `peniakoff/awesome-deploy:jdk11-node14-latest`.

If you need also NodeJS (v18) with npm and yarn, you should use image `peniakoff/awesome-deploy:jdk11-node18-latest`.

If you need Amazon Corretto 8 JDK, you should use image `peniakoff/awesome-deploy:jdk8-latest`.

If you need Amazon Corretto 8 JDK and NodeJS, you should use image `peniakoff/awesome-deploy:jdk8-node14-latest`.

If you need just NodeJS (latest of v14), you should use image `peniakoff/awesome-deploy:node14-latest`.

If you need just NodeJS (latest of v18), you should use image `peniakoff/awesome-deploy:node18-latest`.

If you need more features/tools provided in the images, just open new discuss here https://github.com/peniakoff/awesome-deploy/discussions.
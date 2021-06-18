# AWeSome-deploy
Docker linux image for deployment (eg. via Bitbucket's Pipelines) to AWS

Depends on the branch (and tag) this image contains different tools for deploying your stuff to AWS.
Core for Dockerimage based on the `debian:stable` image and by default contains OpenJDK 11, Maven and Python 3, AWS SAM CLI and AWS CLI.

Default Linux timezone is set to Europe/Warsaw and file encoding is set to UTF-8.

If you need also NodeJS and npm or/and yarn, you should use image from branch 'node'.
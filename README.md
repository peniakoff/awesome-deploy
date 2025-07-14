# AWeSome-deploy

### Docker Linux Images for AWS Deployment

This project provides a suite of Docker images designed for streamlined deployments to Amazon Web Services (AWS), particularly useful in CI/CD environments like Bitbucket Pipelines.

The core of each Docker image is based on `debian:stable`. Common tools included are Python 3, Make, AWS SAM CLI (`v1.142.1`), and AWS CLI. Depending on the image tag, specific versions of Amazon Corretto JDK (8, 11, or 21), Maven, Gradle, and NodeJS (18 or 22 with npm and yarn) are available.

All images are configured with the `Europe/Warsaw` timezone and `UTF-8` file encoding by default. Images with NodeJS also include the AWS CDK for JavaScript/TypeScript projects.

### Available Docker Images

Here's a summary of the currently available Docker images and their pre-installed software:

| Docker Image Tag                               | JDK Version        | NodeJS Version | Key Tools Included                                                                         |
| :--------------------------------------------- | :----------------- | :------------- | :----------------------------------------------------------------------------------------- |
| `peniakoff/awesome-deploy:jdk8-latest`         | Amazon Corretto 8  | N/A            | JDK 8, Maven, Python 3, Make, AWS SAM CLI, AWS CLI                                         |
| `peniakoff/awesome-deploy:jdk8-node18-latest`  | Amazon Corretto 8  | 18             | JDK 8, Maven, NodeJS 18, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK          |
| `peniakoff/awesome-deploy:jdk11-latest`        | Amazon Corretto 11 | N/A            | JDK 11, Maven, Python 3, Make, AWS SAM CLI, AWS CLI                                        |
| `peniakoff/awesome-deploy:jdk11-node18-latest` | Amazon Corretto 11 | 18             | JDK 11, Maven, NodeJS 18, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK         |
| `peniakoff/awesome-deploy:jdk11-node22-latest` | Amazon Corretto 11 | 22             | JDK 11, Maven, NodeJS 22, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK         |
| `peniakoff/awesome-deploy:jdk21-latest`        | Amazon Corretto 21 | N/A            | JDK 21, Maven, Gradle, Python 3, Make, AWS SAM CLI, AWS CLI                                |
| `peniakoff/awesome-deploy:jdk21-node18-latest` | Amazon Corretto 21 | 18             | JDK 21, Maven, NodeJS 18, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK         |
| `peniakoff/awesome-deploy:jdk21-node22-latest` | Amazon Corretto 21 | 22             | JDK 21, Maven, Gradle, NodeJS 22, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK |
| `peniakoff/awesome-deploy:node18-latest`       | N/A                | 18             | NodeJS 18, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK                        |
| `peniakoff/awesome-deploy:node22-latest`       | N/A                | 22             | NodeJS 22, npm, yarn, Python 3, Make, AWS SAM CLI, AWS CLI, AWS CDK                        |

If you need more features or tools provided in the images, please open a new discussion here: https://github.com/peniakoff/awesome-deploy/discussions.

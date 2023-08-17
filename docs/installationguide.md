# Installation Guide

## Requirements

All the components are provided as Dockerized applications, thus the following
software is required:

- Docker
- Docker Compose

!!! info

    We tested our deployment on machines running different configurations:

      - Ubuntu 21, Docker 20.10.8, Docker Compose 1.29.2
      - Ubuntu 22, Docker  24.0.5, Docker Compose 2.20.2

## Install

Before running the containers, it is required to download the Docker images from their respective registries.
While some images are publicly available, some other require credentials to be downloaded from private registries.

!!! faq

    Images can be download from the RAMP Docker registry, which supports the token-based authentication. Please send your
    request for a new token to the RAMP Docker registry maintainers.

Once you are provided with a username and a token, you can issue the following
command to login to the private GitLab Docker registry and download the images:

```shell
docker login docker.ramp.eu -u <username> -p <token>
docker-compose pull <image>:<tag>
```

## Usage

The docker-compose file automatically runs all the components as Docker
containers. Each container can be customized by editing its environment
parameters. The current deployment already set the right values for all the
parameters.

We suggest the user to only modify variables listed in the `.env` file, if
needed.

| Parameter name             | Parameter value | Default |
| -------------------------- | --------------- | ------  |
| BF_USER | A username shared by all the components | **bfuser** |
| BF_PASSWORD | A password shared by all the components | **bfpwd123** |
| MODELS_MYSQL_DATABASE | Name of the database to store the shared model | **models**|
| MODELS_MYSQL_ROOT_PASSWORD | Password for the root user in MySQL | **root** |

Run the **up** command to start all the containers:

```shell
docker-compose up -d
```

You can now access different components:

- Kafka is accessible from the Kafka Development Environment, which is available
  at [localhost:3040](http://localhost:3040/). Here you can check schemas
  uploaded to the Schema Registry, as well as existing Kafka topics and their
  content.

## Software Maintainers

- Vincenzo Cutrona - <vincenzo.cutrona@supsi.ch>
- Giuseppe Landolfi - <giuseppe.landolfi@supsi.ch>

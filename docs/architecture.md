# Architecture

Within the Better Factory project, the FaMS is deployed as part of the Cognitive
Human Robot Interaction (C-HRI) scenario. The deployment is based on Docker
Compose, and the set of initialized components is depicted in the picture here
below:

``` mermaid
flowchart LR
    classDef supsi fill:#B4C7DC;
    classDef pub fill:#B2B2B2
    classDef pvt fill:#E8F2A1

    subgraph SUPSI
    direction TB
    fams:::supsi <--> middleware:::supsi
    kafka-message-model:::supsi --> middleware:::supsi
    end

    subgraph Private Deps
    models:::pvt <--> fams:::supsi
    end

    subgraph Public Deps
    models:::pvt <--> models-db:::pub
    end

```

The blue-colored components represent the core components for which SUPSI
provides and maintains a Docker image; the other components (grey- and
green-colored) represent dependencies that are provided as Docker images by
third parties.

!!! info

    In this deployment version, the only external dependencies that is available
    only in a private registry is *models*. The *models* image is provided and
    maintained by Holonix (HOL) within the Better Factory project.

## Dependencies

### middleware

The image is based on the [fast-data-dev
(v2.6.2)](https://github.com/lensesio/fast-data-dev/tree/fdd/2.6.2) project by
Lenses.io and runs a full fledged Kafka installation (including extra services,
e.g., UIs).

In addition, the Schema Registry is automatically populated with schemas
available under the `/schemas` directory. In our deployment, the `/schemas`
directory is read from the *kafka-message-model* component.

The middleware is run in secure mode and can be accessed at
[localhost:3040](localhost:3040) (credentials are stored in the docker-compose
file).

### kafka-message-model

This component embeds the data model shared within the Better Factory project.
The data model is automatically uploaded to the Schema Registry available within
the *middleware*.

### models

The *models* component exposes a REST API to access the data model shared among
all the components involved in the C-HRI scenario. The API is accessed by the
*fams* component to fetch information about workers and other factory elements.

!!! important

    This image is available in a private Docker registry hosted at GitLab.
    Please ask HOLONIX to get access to this image.

### models-db
The *models-db* component runs an official MySql docker image (v5.7).

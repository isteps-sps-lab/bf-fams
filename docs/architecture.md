# Architecture

Within the Better Factory project, the FaMS is deployed as part of the Cognitive
Human Robot Interaction (C-HRI) scenario. The deployment is based on Docker
Compose, and the set of initialized components is depicted in the picture here
below:

``` mermaid
flowchart LR
    classDef supsi fill:#B4C7DC,color:#000;
    classDef pub fill:#B2B2B2,color:#000;
    classDef pvt fill:#E8F2A1,color:#000;

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

The blue-colored components represent the core components for which SUPSI provides and maintains a Docker image; the other components represent Docker images that are either publicly available (green-colored) or maintened by other Better Factory partners (grey-colored).

!!! info

    In this deployment version, all the Docker images but the public ones can be downloaded from the [RAMP Docker Registry](https://docker.ramp.eu/).

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

### models-db
The *models-db* component runs an official MySql docker image (v5.7).

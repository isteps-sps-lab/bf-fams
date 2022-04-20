# Getting Started

The FaMS and its dependencies are provided as Dockerized applications.

To start the FaMS and its dependencies, issue the **up** command:

```shell
docker-compose up -d
```

The FaMS is a backend application working over Apache Spark, thus a proper UI is
not provided. When new physiological data come, the predicted fatigue level is
published on the middleware.

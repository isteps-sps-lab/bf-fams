# Fatigue Monitoring System (FaMS)

The FaMS component detects possible psychological (e.g., loss of attention,
mental fatigue) or physical (e.g., tiredness) discomfort or harmful situations
for a worker. The situations identified by this component can be targeted by
other modules to trigger short term intervention, i.e., intervention that can be
executed to support a specific worker during the current working shift. Examples
of possible interventions include:

- providing visual support by highlighting which component is the next one to assemble, or where to insert a connector;

- increasing the support provided by the exoskeleton;

- taking a break;

- shut-down all information.


## Getting Started

The FaMS and its dependencies are provided as Dockerized applications.

To start the FaMS and its dependencies, issue the **up** command:

```shell
docker-compose up -d
```

The FaMS is a backend application working over Apache Spark, thus a proper UI is
not provided. When new physiological data come, the predicted fatigue level is
published on the middleware.

## Software Details

- Documentation: https://isteps-sps-lab.github.io/bf-fams/

## Maintainers

- Vincenzo Cutrona - <vincenzo.cutrona@supsi.ch>
- Giuseppe Landolfi - <giuseppe.landolfi@supsi.ch>

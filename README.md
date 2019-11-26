# Hortonworks Schema Registry

## Pre Requisites
* Kubernetes 1.9+
* Requires at least `v3` version of helm to support.
* Required MySQL Server.

# Create a Namespace
```
kubectl create namespace hw-registry
```

# Installing the Chart
To install the chart with the release name my-release, run:

```
helm repo add rubik https://rubik-ai.github.io/hortonworks-registry/package
helm install my-release --namespace=hw-registry rubik/hw-registry
```

The chart can be customized using the following configurable parameters:

| Parameter                       | Description                                                     | Default                      |
|---------------------------------|-----------------------------------------------------------------|------------------------------|
|image.repository                 |Hortonworks Container image name                                 | `rubiklabs/hortonworks-registry` |
|image.tag                        |Container image tag                                              | `v0.3.0`                         |
|image.pullPolicy                 |Container pull policy                                            | `IfNotPresent`                   |
|namespace                        |Pod deploy on namespace                                          | `default`                        |
|replicaCount                     |Number of replicas                                               | `1`                              |
|service.type                     |Kubernetes Service type                                          | `ClusterIP`                      |
|service.port                     |Port for kubernetes service                                      | `9090`                           |
|terminationGracePeriodSeconds    |Wait time before forcefully terminating container                | `30`                             |

## Environment Variables
| Parameter                       | Description                                                     | Default                      |
|---------------------------------|-----------------------------------------------------------------|------------------------------|
|environment.sql_user             |MySQL database user.                                             | `hortonworks`                |
|environment.sql_db               |MySQL database name.                                             | `hortonworks`                |
|environment.sql_password         |MySQL password.                                                  | `hortonworks`                |
|environment.sql_host             |MySQL Hostname.                                                  | `db`                         |
|environment.sql_port             |MySQL Port.                                                      | `3306`                       |

Specify parameters using --set key=value[,key=value] argument to helm install
Alternatively a YAML file that specifies the values for the parameters can be provided like this:
```
helm install my-release -f values.yaml rubik/hw-registry
```
> **Tip**: You can use the default [values.yaml](values.yaml)

# Uninstalling the Chart
To uninstall/delete the my-release deployment:
```
helm delete my-release
```

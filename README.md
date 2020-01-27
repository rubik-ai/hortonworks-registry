# Hortonworks Schema Registry

## Pre Requisites
* Kubernetes 1.9+
* Requires at least `v3` version of helm to support.
* Required MySQL Server 5.7 and above.

## Add Namespace Plugin
Installation is as simple as running:

```bash
helm plugin install https://github.com/thomastaylor312/helm-namespace
```

*  Note:- please refer to more information [*Click Here.*](https://github.com/thomastaylor312/helm-namespace)

# Installing the Chart
To install the chart with the release name hw-registry, run:

```bash
helm repo add rubik https://rubik-ai.github.io/hortonworks-registry/package
helm repo update
helm search repo rubik
helm namespace install hw-registry rubik/hw-registry --namespace=hw-registry
```

The chart can be customized using the following configurable parameters:

| Parameter                       | Description                                                     | Default                      |
|---------------------------------|-----------------------------------------------------------------|------------------------------|
|image.repository                 |Hortonworks Container image name                                 | `rubiklabs/hortonworks-registry` |
|image.tag                        |Container image tag                                              | `v0.3.0`                         |
|image.pullPolicy                 |Container pull policy                                            | `IfNotPresent`                   |
|replicaCount                     |Number of replicas                                               | `1`                              |
|service.type                     |Kubernetes Service type                                          | `ClusterIP`                      |
|service.port                     |Port for kubernetes service                                      | `9090`                           |
|restartPolicy                    |Pod Restart Policy                                               | `Always`                  |
|terminationGracePeriodSeconds    |Wait time before forcefully terminating container                | `30`                             |

## Environment Variables to connect MySQL Server.
| Parameter                       | Description                                                     | Default                      |
|---------------------------------|-----------------------------------------------------------------|------------------------------|
|environment.sql_user             |MySQL database user.                                             | `root`                |
|environment.sql_db               |MySQL database name.                                             | `hortonworks`                |
|environment.sql_password         |MySQL password.                                                  | `hortonworks`                |
|environment.sql_host             |MySQL Hostname.                                                  | `db`                         |
|environment.sql_port             |MySQL Port.                                                      | `3306`                       |

Specify parameters using --set key=value[,key=value] argument to helm install
Alternatively a YAML file that specifies the values for the parameters can be provided like this:

```bash
helm namespace install hw-registry -f values.yaml rubik/hw-registry
```

> **Tip**: You can use the default [values.yaml](values.yaml)

Check you deployedment with helm command:

```bash
helm list --namespace=hw-registry
```

# Uninstalling the Chart
To uninstall/delete the hw-registry deployment:

```bash
helm delete hw-registry --namespace=hw-registry
```
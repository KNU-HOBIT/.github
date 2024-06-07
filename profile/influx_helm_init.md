# InfluxDB Helm Chart

This guide contains the Helm chart for deploying InfluxDB using Kubernetes.

## Introduction
This Helm chart allows you to deploy InfluxDB, a powerful time-series database, on a Kubernetes cluster. The chart provides customizable configurations to manage persistence, storage class, service type, and node ports.

[reference](https://github.com/influxdata/helm-charts/tree/master/charts/influxdb
)

## Prerequisites
- Kubernetes cluster
- Helm installed and configured
- Persistent storage configured in your cluster (e.g., rook-ceph)

## Installation
To install the InfluxDB Helm chart, use the following command:

```sh
helm upgrade --install influxdb \
  --set persistence.enabled=true,persistence.size=200Gi,persistence.storageClass=rook-cephfs,service.type=NodePort,service.nodePorts.http=32145 \
  influxdata/influxdb2 -n influxdb
```
### Configuration

The chart can be configured using a values file or through the --set flag during installation. Key configuration options include:

- `persistence.enabled`: Enable or disable persistent storage
- `persistence.size`: Specify the size of the persistent storage
- `persistence.storageClass`: Define the storage class for persistent storage
- `service.type`: Set the type of service (e.g., NodePort)
- `service.nodePorts.http`: Define the node port for HTTP service

### Checking Admin Password
To retrieve the admin password for InfluxDB, use the following command:

```sh
echo $(kubectl get secret influxdb-influxdb2-auth -o "jsonpath={.data['admin-password']}" --namespace influxdb | base64 --decode)
```


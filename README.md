# kustomize-spark-operator

A Kustomize module for the Spark Operator.

This repo is a bespoke configuration of the [Spark Operator](https://github.com/GoogleCloudPlatform/spark-on-k8s-operator) targets configured for high availability and scalability for GKE.

It is meant to be used as a module in your [Kustomize](https://github.com/kubernetes-sigs/kustomize) configuration.

## Project Status

**Project status:** *beta*

The Kubernetes Operator for Apache Spark is under active development, but backward compatibility of the APIs is guaranteed for beta releases.

## Prerequisites

* Version >= 1.13 of Kubernetes to use the [`subresource` support for CustomResourceDefinitions](https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/#subresources), which became beta in 1.13 and is enabled by default in 1.13 and higher.

## Installation the manifests

The manifests can be installed using kustomize by running:

```bash
kustomize build . | kubectl apply -f -
```

## Configuration

The following table lists the configurable parameters of the Spark operator chart and their default values.

| Parameter                 | Description                                                  | Default                                |
| ------------------------- | ------------------------------------------------------------ | -------------------------------------- |
| `sparkjob-namespace`      | K8s namespace where Spark jobs are to be deployed            | `spark-jobs`                           |
| `enable-webhook`          | Whether to enable mutating admission webhook                 | true                                   |
| `enable-metrics`          | Whether to expose metrics to be scraped by Premetheus        | true                                   |
| `controller-threads`      | Number of worker threads used by the SparkApplication controller | 10                                 |
| `ingress-url`             | Ingress URL format                                           | ""                                     |                                    |                                |
| `metrics-port`            | Port for the metrics endpoint                                | 10254                                  |
| `metrics-endpoint`        | Metrics endpoint                                             | "/metrics"                             |
| `metrics-prefix`          | Prefix for the metrics                                       | ""                                     |
| `resync-interval`         | Informer resync interval in seconds                          | 30                                     |
| `webhook-port`            | Service port of the webhook server                           | 8080                                   |
| `enable-batch-scheduler`  | Whether to enable batch scheduler for pod scheduling         | true                                   |                                 |
| `leader-election`         | Whether to enable leader election when the operator Deployment has more than one replica, i.e., when `replicas` is greater than 1.         | true                                  |

Specify each parameter by copying [sparkoperator-config.properties](base/spark-operator/sparkoperator-config.properties) to an overlay and adapt the values.

Note that the default namespace for the operator is `spark-operator` and for the spark-jobs (created by the operator) `spark-jobs`. This can be overrided in a kustomization.yaml in your own installation. If you change these, make sure you update the values in [sparkoperator-config.properties](base/spark-operator/sparkoperator-config.properties as well.

## Get Started

Get started quickly with the Kubernetes Operator for Apache Spark using the [Quick Start Guide](https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/master/docs/quick-start-guide.md).

## Contributing

Please check [CONTRIBUTING.md](CONTRIBUTING.md) out.

# K6 TIG Helm Chart

## Defenition:

A Helm chart is a package that contains all the necessary resources to deploy an application to a Kubernetes cluster. This includes YAML configuration files for deployments, services, secrets, and config maps that define the desired state of your application.

## Introduction

This Helm Chart deploys a comprehensive monitoring and visualization stack for k6 load testing, leveraging the power of Telegraf, StatsD, InfluxDB, and Grafana. It provides a seamless solution for performance testing, metrics collection, aggregation, storage, and dashboarding.

The chart contains deployemnt files for k6, telegraf, and influxdb. And will assume that you have grafana preconfigured and installed in your cluster.

## Requirements:

1. Helm 3.0
2. A wokring kubernetes cluster with the right access
3. Grafana running on the cluster
4. k6 script (a default is provided)
5. Telegraf configuration file (a default is provided with statsd plugin)

## Add the chart

### Expose nexus service

Keep this port exposed as long as you are using the chart, when you finish deploying it you can close this port.

	kubectl port-forward services/nexus 8081:8081 -n central

### Add repository

	helm repo add helm-hosted http://localhost:8081/repository/helm-hosted/ --username helm --password PASSWORD

### Save values.yaml file

	helm show values helm-hosted/k6-tig-chart > values.yaml

## Edit the values.yaml

The current values.yaml file will work fine without any editing.

## Install the chart

	helm install ktig helm-hosted/k6-tig-chart -n NAMESPACE

### To pass edited values.yaml file:

	helm install ktig helm-hosted/k6-tig-chart -n NAMESPACE -f values.yaml

### To unsintall the chart

	helm unsintall ktig -n NAMESPACE


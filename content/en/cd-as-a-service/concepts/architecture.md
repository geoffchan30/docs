---
title: Armory Continuous Deployment-as-a-Service Architecture
linkTitle: Architecture
description: >
  Armory Continuous Deployment-as-a-Service Architecture
exclude_search: true
weight: 10
aliases:
  - /armory-deployments/architecture/
---

## Key Components

### Remote Network Agent (RNA)

The RNA allows Armory CD-as-a-Service to interact with your Kubernetes clusters and orchestrate deployments without direct network access to your clusters. The RNA that you install in your cluster engages in bidirectional communication with Armory CD-as-a-Service over encrypted, long-lived gRPC/HTTP2 connections. The RNA issues calls to your Kubernetes cluster based on requests from Armory CD-as-a-Service.

### Command Line Interface (CLI)

Users install the CLI locally. The CLI interacts with Armory CD-as-a-Service via REST API. To deploy an app, the user must either log in using the CLI or pass valid authorization credentials to the `deploy` command.

### GitHub Action (GHA)

You can use the `armory/cli-deploy-action` to trigger a deployment from your GitHub workflow. The GitHub Action interacts with Armory CD-as-a-Service via REST API. The Action requires a valid Client ID and Client Secret be passed to the deploy command.

### Spinnaker plugin

{{< include "cdaas/desc-plugin.md" >}}

## How Armory CD-as-a-Service works

Armory CD-as-a-Service is a platform of cloud-based services that orchestrate app deployments and monitor their progress. These services have API endpoints with which users and non-cloud services interact via HTTPS or gRPC/HTTP2. The [Networking](#networking) section contains details of the endpoints that need to be whitelisted.

Armory CD-as-a-Service contains components that you manage: the CLI, the RNA, and the GHA. These components communicate with Armory CD-as-a-Service to deploy your apps to your existing infrastructure.

{{< include "cdaas/mermaid/how-it-works.md" >}}

When you start a deployment from the CLI or the GHA, Armory CD-as-a-Service forwards your deployment request to the designated RNA in your Kubernetes cluster. The RNA generates Kubernetes Custom Resource Definitions that it then uses to execute the deployment.

You can track the status of a deployment in the Armory CD-as-a-Service UI.

## Networking

{{< include "cdaas/req-networking.md" >}}

## {{% heading "nextSteps" %}}

{{< linkWithTitle "cd-as-a-service/setup/get-started.md" >}}

<br>
<br>
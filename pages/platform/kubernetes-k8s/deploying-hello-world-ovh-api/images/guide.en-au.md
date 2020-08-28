---
title: Deploying a Hello World with the OVH API
slug: deploying-hello-world-ovh-api
excerpt: 'Find out how to deploy a Hello World application with the OVH API'
section: Tutorials
order: 2
---

**Last updated 1<sup>st</sup> July, 2019.**

Follow this quickstart guide to deploy a containerised *Hello World* application on your OVHcloud Managed Kubernetes Service cluster, using the OVH API.

In this guide, we are assuming you're using the [OVHcloud API](https://api.ovh.com/) to manage your Kubernetes cluster. If you are using a different method, like the [OVHcloud Cloud Manager](https://ca.ovh.com/auth/?action=gotomanager), please refer to the relevant documentation:

- [Deploying a Hello World application with the OVHcloud Cloud Manager](../deploying-hello-world/)

## Before you begin

* You should have already created a cluster on the OVHcloud Managed Kubernetes service.
* You will also need the [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/){.external} command-line tool. You can find the [detailed installation instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl/){.external} for this tool on Kubernetes' official site.

> [!warning]
> This guide assumes you are familiar with the [OVH API](https://api.ovh.com/). If you have never used it, you can find the basics here: [First steps with the OVH API](https://docs.ovh.com/gb/en/customer/first-steps-with-ovh-api/).
>

## The API Explorer

To simplify things, we are using the [API Explorer](https://api.ovh.com/console/), which allows to explore, learn and interact with the API in an interactive way.

Log in to the API Explorer using your OVH NIC.

![Log in to the API Explorer](images/kubernetes-quickstart-api-ovh-com-001.png){.thumbnail}

If you go to the [Kubernetes section](https://api.ovh.com/console/#/kube) of the API Explorer, you will see the available endpoints:

![Kubernetes section of the API Explorer](images/kubernetes-quickstart-api-ovh-com-002.png){.thumbnail}


## List your OVHcloud Managed Kubernetes clusters

The `GET /cloud/project` API endpoint lists all the available Public Cloud Services associated to your OVHcloud account:

![List your OVHcloud Public Cloud Services](images/kubernetes-quickstart-api-ovh-com-003.png){.thumbnail}

Choose the Public Cloud Service corresponding to your OVHcloud Managed Kubernetes. In this example, we will refer to it as `serviceName`

The `GET /cloud/project/{serviceName}/kube` API endpoint lists all the available clusters in your chosen project:

![List your OVHcloud Managed Kubernetes clusters](images/kubernetes-quickstart-api-ovh-com-004.png){.thumbnail}

By calling it, you can view a list of your Kubernetes clusters ID. Note down the ID of the cluster you want to use. In this example, we will refer to it as `kubeId`


## Getting your cluster information

The `GET  /cloud/project/{serviceName}/kube/{kubeId}` API endpoint provides important information about your OVHcloud Managed Kubernetes cluster, including its status and URL.

![Getting your cluster information in the OVHcloud API](images/kubernetes-quickstart-api-ovh-com-005.png){.thumbnail}


## Listing node pools


The `GET /cloud/project/{serviceName}/kube/{kubeId}/nodepool` API endpoint lists all the available node pools:

![Listing node pools](images/kubernetes-quickstart-api-ovh-com-006.png){.thumbnail}

## Create a node pool with at least one node

The first element needed to deploy the *Hello World* application is a worker node in your cluster. To create this node pool, you can use the use the `POST /cloud/project/{serviceName}/kube/{kubeId}/nodepool` API endpoint to create a new node pool:

You will need to give it a `flavorName` parameter, with the flavor of the instance you want to create. For this tutorial choose a general purpose node, like the `b2-7` flavor.

As you want your node pool to have at least one node, set the `desiredSize` to a value above 0.

The API will return you the new node pool information.

![Create a node pool](images/kubernetes-quickstart-api-ovh-com-007.png)

## Verify your node is ready

You can use the `GET  /cloud/project/{serviceName}/kube/{kubeId}/nodepool/{nodePoolId}` endpoint to get information on a node pool. Verify the status is `READY`. The node pool installation can take a minute, so feel free to take a small break, then try again until it's ready.

![Verify your node is ready](images/kubernetes-quickstart-api-ovh-com-008.png){.thumbnail}

## Configuring the default settings for kubectl

Please refer to the [Configuring kubectl on an OVHcloud Managed Kubernetes cluster](../configuring-kubectl/) documentation for this part of the process.

## Deploy your first application

You're now ready to deploy your first application.

For more details about this process, you can refer to the [deploying an application](../deploying-an-application/) documentation.
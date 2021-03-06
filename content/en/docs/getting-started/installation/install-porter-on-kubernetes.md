---
title: "Install Porter on Kubernetes (kubectl and Helm)"
linkTitle: "Install Porter on Kubernetes (kubectl and Helm)"
weight: 1
---

This document describes how to use kubectl and [Helm](https://helm.sh/) to install and delete Porter in a Kubernetes cluster. For details about how to install and delete Porter on the [KubeSphere](https://kubesphere.io/docs/installing-on-linux/introduction/multioverview/#step-3-create-a-cluster) web console, see [Install Porter on KubeSphere (Web Console)](/docs/getting-started/installation/install-porter-on-kubesphere/).

## Prerequisites

* You need to prepare a Kubernetes cluster, and ensure that the Kubernetes version is 1.15 or later. Porter requires CustomResourceDefinition (CRD) v1, which is only supported by Kubernetes 1.15 or later. You can use the following methods to deploy a Kubernetes cluster:

  * Use [KubeKey](https://kubesphere.io/docs/installing-on-linux/) (recommended). You can use KubeKey to deploy a Kubernetes cluster with or without KubeSphere.
  * Follow [official Kubernetes guides](https://kubernetes.io/docs/home/).

  Porter is designed to be used in bare-metal Kubernetes environments. However, you can also use a cloud-based Kubernetes cluster for learning and testing.

* If you use Helm to install porter, ensure that the Helm version is Helm 3.

## Install Porter Using kubectl

1. Log in to the Kubernetes cluster over SSH and run the following command:

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/kubesphere/porter/master/deploy/porter.yaml
   ```
   
2. Run the following command to check whether the status of porter-manager is **READY**: **1/1** and **STATUS**: **Running**. If yes, Porter has been installed successfully.

   ```bash
   kubectl get po -n porter-system
   ```

   ![verify-porter-kubectl](/images/docs/getting-started/installation/install-porter-on-kubernetes/verify-porter-kubectl.jpg)

## Delete Porter Using kubectl

1. To delete Porter, log in to the Kubernetes cluster and run the following command:

   ```bash
   kubectl delete -f https://raw.githubusercontent.com/kubesphere/porter/master/deploy/porter.yaml
   ```

   {{< notice note >}}

   Before deleting Porter, you must first delete all services that use Porter.

   {{</ notice >}}

2. Run the following command to check the result. If the porter-system name space does not exist, Porter has been deleted successfully.

   ```bash
   kubectl get ns
   ```
   
   ![verify-porter-deletion-kubectl](/images/docs/getting-started/installation/install-porter-on-kubernetes/verify-porter-deletion-kubectl.jpg)

## Install Porter Using Helm

1. Log in to the Kubernetes cluster over SSH and run the following commands:

   ```bash 
   helm repo add test https://charts.kubesphere.io/test
   helm repo update
   helm install porter test/porter
   ```

2. Run the following command to check whether the status of porter-manager is **READY**: **1/1** and **STATUS**: **Running**. If yes, Porter has been installed successfully.

   ```bash
   kubectl get po -A
   ```

   ![verify-porter-helm](/images/docs/getting-started/installation/install-porter-on-kubernetes/verify-porter-helm.jpg)

## Delete Porter Using Helm

1. To delete Porter, run the following command:

   ```bash
   helm delete porter
   ```

   {{< notice note >}}

   Before deleting Porter, you must first delete all services that use Porter.

   {{</ notice >}}

2. Run the following command to check the result. If the Porter application does not exist, Porter has been deleted successfully.

   ```bash
   helm ls
   ```

   ![verify-porter-deletion-helm](/images/docs/getting-started/installation/install-porter-on-kubernetes/verify-porter-deletion-helm.jpg)
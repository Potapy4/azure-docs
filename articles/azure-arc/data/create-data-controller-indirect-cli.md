---
title: Create data controller using CLI
description: Create an Azure Arc data controller, on a typical multi-node Kubernetes cluster which you already have created, using the CLI.
services: azure-arc
ms.service: azure-arc
ms.subservice: azure-arc-data
author: dnethi
ms.author: dinethi
ms.reviewer: mikeray
ms.date: 07/13/2021
ms.topic: how-to
---

# Create Azure Arc data controller using the CLI

[!INCLUDE [azure-arc-data-preview](../../../includes/azure-arc-data-preview.md)]

## Prerequisites

Review the topic [Create the Azure Arc data controller](create-data-controller.md) for overview information.

To create the Azure Arc data Controller using the [!INCLUDE [azure-data-cli-azdata](../../../includes/azure-data-cli-azdata.md)] you will need to have the [!INCLUDE [azure-data-cli-azdata](../../../includes/azure-data-cli-azdata.md)] installed.

   [Install the [!INCLUDE [azure-data-cli-azdata](../../../includes/azure-data-cli-azdata.md)]](install-client-tools.md)

Regardless of which target platform you choose, you will need to set the following environment variables prior to the creation for the data controller administrator user. You can provide these credentials to other people that need to have administrator access to the data controller as needed.

**AZDATA_USERNAME** - A username of your choice for the data controller administrator user. Example: `arcadmin`

**AZDATA_PASSWORD** - A password of your choice for the data controller administrator user. The password must be at least eight characters long and contain characters from three of the following four sets: uppercase letters, lowercase letters, numbers, and symbols.

### Linux or macOS

```console
export AZDATA_USERNAME="<your username of choice>"
export AZDATA_PASSWORD="<your password of choice>"
```

### Windows PowerShell

```console
$ENV:AZDATA_USERNAME="<your username of choice>"
$ENV:AZDATA_PASSWORD="<your password of choice>"
```

You will need to connect and authenticate to a Kubernetes cluster and have an existing Kubernetes context selected prior to beginning the creation of the Azure Arc data controller. How you connect to a Kubernetes cluster or service varies. See the documentation for the Kubernetes distribution or service that you are using on how to connect to the Kubernetes API server.

You can check to see that you have a current Kubernetes connection and confirm your current context with the following commands.

```console
kubectl get namespace
kubectl config current-context
```

## Create the Azure Arc data controller

> [!NOTE]
> You can use a different value for the `--namespace` parameter of the `azdata arc dc create` command in the examples below, but be sure to use that namespace name for the `--namespace parameter` in all other commands below.

- [Create Azure Arc data controller using the CLI](#create-azure-arc-data-controller-using-the-cli)
  - [Prerequisites](#prerequisites)
    - [Linux or macOS](#linux-or-macos)
    - [Windows PowerShell](#windows-powershell)
  - [Create the Azure Arc data controller](#create-the-azure-arc-data-controller)
    - [Create on Azure Kubernetes Service (AKS)](#create-on-azure-kubernetes-service-aks)
    - [Create on AKS engine on Azure Stack Hub](#create-on-aks-engine-on-azure-stack-hub)
    - [Create on AKS on Azure Stack HCI](#create-on-aks-on-azure-stack-hci)
    - [Create on Azure Red Hat OpenShift (ARO)](#create-on-azure-red-hat-openshift-aro)
      - [Create custom deployment profile](#create-custom-deployment-profile)
      - [Create data controller](#create-data-controller)
    - [Create on Red Hat OpenShift Container Platform (OCP)](#create-on-red-hat-openshift-container-platform-ocp)
      - [Determine storage class](#determine-storage-class)
      - [Create custom deployment profile](#create-custom-deployment-profile-1)
      - [Set storage class](#set-storage-class)
      - [Set LoadBalancer (optional)](#set-loadbalancer-optional)
      - [Create data controller](#create-data-controller-1)
    - [Create on open source, upstream Kubernetes (kubeadm)](#create-on-open-source-upstream-kubernetes-kubeadm)
    - [Create on AWS Elastic Kubernetes Service (EKS)](#create-on-aws-elastic-kubernetes-service-eks)
    - [Create on Google Cloud Kubernetes Engine Service (GKE)](#create-on-google-cloud-kubernetes-engine-service-gke)
  - [Monitoring the creation status](#monitoring-the-creation-status)
  - [Troubleshooting creation problems](#troubleshooting-creation-problems)

### Create on Azure Kubernetes Service (AKS)

By default, the AKS deployment profile uses the `managed-premium` storage class. The `managed-premium` storage class will only work if you have VMs that were deployed using VM images that have premium disks.

If you are going to use `managed-premium` as your storage class, then you can run the following command to create the data controller. Substitute the placeholders in the command with your resource group name, subscription ID, and Azure location.

```console
azdata arc dc create --profile-name azure-arc-aks-premium-storage --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-aks-premium-storage --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

If you are not sure what storage class to use, you should use the `default` storage class which is supported regardless of which VM type you are using. It just won't provide the fastest performance.

If you want to use the `default` storage class, then you can run this command:

```console
azdata arc dc create --profile-name azure-arc-aks-default-storage --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-aks-default-storage --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

### Create on AKS engine on Azure Stack Hub

By default, the deployment profile uses the `managed-premium` storage class. The `managed-premium` storage class will only work if you have worker VMs that were deployed using VM images that have premium disks on Azure Stack Hub.

You can run the following command to create the data controller using the managed-premium storage class:

```console
azdata arc dc create --profile-name azure-arc-aks-premium-storage --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-aks-premium-storage --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

If you are not sure what storage class to use, you should use the `default` storage class which is supported regardless of which VM type you are using. In Azure Stack Hub, premium disks and standard disks are backed by the same storage infrastructure. Therefore, they are expected to provide the same general performance, but with different IOPS limits.

If you want to use the `default` storage class, then you can run this command.

```console
azdata arc dc create --profile-name azure-arc-aks-default-storage --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-aks-default-storage --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

### Create on AKS on Azure Stack HCI

By default, the deployment profile uses a storage class named `default` and the service type `LoadBalancer`.

You can run the following command to create the data controller using the `default` storage class and service type `LoadBalancer`.

```console
azdata arc dc create --profile-name azure-arc-aks-hci --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-aks-hci --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).


### Create on Azure Red Hat OpenShift (ARO)

#### Create custom deployment profile

Use the profile `azure-arc-azure-openshift` for Azure RedHat Open Shift.

```console
azdata arc dc config init --source azure-arc-azure-openshift --path ./custom
```

#### Create data controller

You can run the following command to create the data controller:

```console
azdata arc dc create --profile-name azure-arc-azure-openshift --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example
#azdata arc dc create --profile-name azure-arc-azure-openshift --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

### Create on Red Hat OpenShift Container Platform (OCP)

> [!NOTE]
> If you are using Red Hat OpenShift Container Platform on Azure, it is recommended to use the latest available version.

#### Determine storage class

You will also need to determine which storage class to use by running the following command.

```console
kubectl get storageclass
```

#### Create custom deployment profile

Create a new custom deployment profile file based on the `azure-arc-openshift` deployment profile by running the following command. This command creates a directory `custom` in your current working directory and a custom deployment profile file `control.json` in that directory.

Use the profile `azure-arc-openshift` for OpenShift Container Platform.

```console
azdata arc dc config init --source azure-arc-openshift --path ./custom
```

#### Set storage class 

Now, set the desired storage class by replacing `<storageclassname>` in the command below with the name of the storage class that you want to use that was determined by running the `kubectl get storageclass` command above.

```console
azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.data.className=<storageclassname>"
azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.logs.className=<storageclassname>"

#Example:
#azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.data.className=mystorageclass"
#azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.logs.className=mystorageclass"
```

#### Set LoadBalancer (optional)

By default, the `azure-arc-openshift` deployment profile uses `NodePort` as the service type. If you are using an OpenShift cluster that is integrated with a load balancer, you can change the configuration to use the `LoadBalancer` service type using the following command:

```console
azdata arc dc config replace --path ./custom/control.json --json-values "$.spec.services[*].serviceType=LoadBalancer"
```

#### Create data controller

Now you are ready to create the data controller using the following command.

> [!NOTE]
>   The `--path` parameter should point to the _directory_ containing the control.json file not to the control.json file itself.


```console
azdata arc dc create --path ./custom --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --path ./custom --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

### Create on open source, upstream Kubernetes (kubeadm)

By default, the kubeadm deployment profile uses a storage class called `local-storage` and service type `NodePort`. If this is acceptable you can skip the instructions below that set the desired storage class and service type and immediately run the `azdata arc dc create` command below.

If you want to customize your deployment profile to specify a specific storage class and/or service type, start by creating a new custom deployment profile file based on the kubeadm deployment profile by running the following command. This command will create a directory `custom` in your current working directory and a custom deployment profile file `control.json` in that directory.

```console
azdata arc dc config init --source azure-arc-kubeadm --path ./custom
```

You can look up the available storage classes by running the following command.

```console
kubectl get storageclass
```

Now, set the desired storage class by replacing `<storageclassname>` in the command below with the name of the storage class that you want to use that was determined by running the `kubectl get storageclass` command above.

```console
azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.data.className=<storageclassname>"
azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.logs.className=<storageclassname>"

#Example:
#azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.data.className=mystorageclass"
#azdata arc dc config replace --path ./custom/control.json --json-values "spec.storage.logs.className=mystorageclass"
```

By default, the kubeadm deployment profile uses `NodePort` as the service type. If you are using a Kubernetes cluster that is integrated with a load balancer, you can change the configuration using the following command.

```console
azdata arc dc config replace --path ./custom/control.json --json-values "$.spec.services[*].serviceType=LoadBalancer"
```

Now you are ready to create the data controller using the following command.

```console
azdata arc dc create --path ./custom --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --path ./custom --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

### Create on AWS Elastic Kubernetes Service (EKS)

By default, the EKS storage class is `gp2` and the service type is `LoadBalancer`.

Run the following command to create the data controller using the provided EKS deployment profile.

```console
azdata arc dc create --profile-name azure-arc-eks --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-eks --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

### Create on Google Cloud Kubernetes Engine Service (GKE)

By default, the GKE storage class is `standard` and the service type is `LoadBalancer`.

Run the following command to create the data controller using the provided GKE deployment profile.

```console
azdata arc dc create --profile-name azure-arc-gke --namespace arc --name arc --subscription <subscription id> --resource-group <resource group name> --location <location> --connectivity-mode indirect

#Example:
#azdata arc dc create --profile-name azure-arc-gke --namespace arc --name arc --subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --resource-group my-resource-group --location eastus --connectivity-mode indirect
```

Once you have run the command, continue on to [Monitoring the creation status](#monitoring-the-creation-status).

## Monitoring the creation status

Creating the controller will take a few minutes to complete. You can monitor the progress in another terminal window with the following commands:

> [!NOTE]
>  The example commands below assume that you created a data controller and Kubernetes namespace with the name `arc`. If you used a different namespace/data controller name, you can replace `arc` with your name.

```console
kubectl get datacontroller/arc --namespace arc
```

```console
kubectl get pods --namespace arc
```

You can also check on the creation status of any particular pod by running a command like below. This is especially useful for troubleshooting any issues.

```console
kubectl describe po/<pod name> --namespace arc

#Example:
#kubectl describe po/control-2g7bl --namespace arc
```

## Troubleshooting creation problems

If you encounter any troubles with creation, see the [troubleshooting guide](troubleshoot-guide.md).
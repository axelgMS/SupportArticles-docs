---
title: Troubleshoot the AKSCapacityError error code
description: Troubleshoot the AKSCapacityError error when you create or start a Kubernetes cluster.
ms.date: 03/27/2024
author: axelgMS
ms.author: axelg
editor: 
ms.reviewer: chiragpa, 
ms.service: azure-kubernetes-service
ms.subservice: troubleshoot-create-operations
---
# Troubleshoot the AKSCapacityError error code

This article describes how to identify and resolve the `AKSCapacityError` error that might occur when you create or start a Microsoft Azure Kubernetes Service (AKS) cluster.

## Symptoms

When you try to create or start an AKS cluster, you receive the following error message:

> Code: AKSCapacityError
>
> Message: Creating a new cluster or start cluster is unavailable at this time in region westeurope. To create a new cluster, we recommend using an alternate region. For a list of all the Azure regions, visit https://aka.ms/aks/regions.



## Cause : Limited capacity in the region

You're trying to deploy a cluster in a region that has limited capacity at the time of the operation. 

When you create or start an AKS cluster, Microsoft Azure allocates compute resources to your subscription. 
We are continually investing in additional infrastructure and features to make sure that we always have all resources available to support customer demand. 
However, you may occasionally experience AKSCapacityError because of unprecedented growth in demand for Azure Kubernetes Service in specific regions. 


## Solution 1: Use a different region

The easiest & quickest solution is to try deploying to a different region that has enough capacity at the given time (eg. NorthEurope instead of WestEurope).

While we understand this might not be feasible if you already have existing resources in the requested region, this is the preferred solution if you're creating a cluster for a Dev/Test scenario.

## Solution 2: Retry the operation

Capacity is often reclaimed when other users are stopping or deleting their AKS clusters, so you can always retry later until the operation succeeds.

## Solution 3: Use an Azure Enterprise subscription

When capacity is running low, Free & Trial subscriptions will be limited first to ensure resources are reserved for real production scenarios. 
So ensure you are creating your AKS cluster with an Enterprise subscription (EA = Enterprise Agreement).

## Solution 4: Try deploying a cluster with different settings

Our underlays hosting the AKS control planes might have different allocation reservations, and so the underlays for public AKS clusters might have more capacity than the ones for Private clusters.
So if you are facing the AKSCapacityError with a private cluster, you can try creating a public one instead.



## More information

- [General troubleshooting of AKS cluster creation issues](troubleshoot-aks-cluster-creation-issues.md)

[!INCLUDE [Azure Help Support](../../includes/azure-help-support.md)]

# Kubernetes Advanced Scheduling Lab

If you are reading this, welcome! We will be reviewing ways to influence scheduling in Kubernetes.

## Requirements

1. Google Cloud Platform Project
2. gcloud SDK
3. Google Kubernetes Engine Cluster in a Single Zone

Please note that there are respective billing costs associated with running resources in Google Cloud Platform.

## Expectations 

In this lab, we will do the following:

1. Add a Node Pool to our GKE cluster with Taints
2. Observe Taint Effect
3. Apply Toleration and NodeAffinity to a given Workload
4. Observe Toleration and NodeAffinity Effect
5. Create Resource Quotas in a Namespace
6. Observe Resource Quota Effect
7. Create a Validating Admission Webhook
8. Observe Validating Admission Webhook Effect

### Add Node Pool with Taints

In your Google Kubernetes Engine cluster, you should have one or more node pools. In order to demonstrate advanced scheduling techniques, we will add a different node pool with Taints. 

Taints function on behalf of a given node, in order to prevent workloads from being scheduled on that node. Taints are represented as [KEY]=[VALUE]:[EFFECT], with [KEY] and [VALUE] as an arbitrary kv pair and [EFFECT] as either PreferNoSchedule, NoSchedule, or NoExecute. 

This is particularly useful for intensive workloads that have special requirements, be it more CPU or hardware acceleration. 

We will now create a Node Pool titled advanced-pool. 

```
gcloud container node-pools create advanced-pool \
--cluster [CLUSTER_NAME] --zone [COMPUTE_ZONE] \ 
--num-nodes 2 --machine-type n1-standard-1 \
--node-taints advanced=workload:NoSchedule
```
Our nodes will now have a Taint, prohibiting workloads to be scheduled on these nodes.

### Deploy Nginx with No Toleration 

Let us now 

### Deploy Nginx with Toleration



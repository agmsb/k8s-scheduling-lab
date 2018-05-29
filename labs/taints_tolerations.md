## Taints and Tolerations Lab

### Add Node Pool with Taints

In your Google Kubernetes Engine cluster, you should have one or more node pools. In order to demonstrate advanced scheduling techniques, we will add a different node pool with Taints. 

Taints function on behalf of a given node, in order to prevent workloads from being scheduled on that node. Taints are represented as [KEY]=[VALUE]:[EFFECT], with [KEY] and [VALUE] as an arbitrary kv pair and [EFFECT] as either PreferNoSchedule, NoSchedule, or NoExecute. 

This is particularly useful for intensive workloads that have special requirements, be it more CPU or hardware acceleration. 

Create a Node Pool titled "advanced-pool" with the Taint "dedicated=advanced:NoSchedule". 

```
gcloud container node-pools create advanced-pool \
--cluster [CLUSTER_NAME] --zone [COMPUTE_ZONE] \ 
--num-nodes 2 --machine-type n1-standard-1 \
--node-taints dedicated=advanced:NoSchedule
```
The nodes will now have a Taint, prohibiting workloads without an appropriate toleration to be scheduled on these nodes.

### Deploy Nginx with No Toleration 

Deploy an nginx pod using a Deployment named "nginx-none" to observe the Taint in action. You can view the .yaml [here](https://github.com/agmsb/k8s-scheduling-lab/blob/master/kubernetes/deployments/nginx.yaml).

```
kubectl apply -f kubernetes/deployments/nginx.yaml
```

Now get the pod resource to see what node it was scheduled on.

```
kubectl get po -o wide
```
You should see the nginx-none pod running on a node in a Node Pool that is not titled "advanced-pool". That is the Taint in action. Feel free to create other arbitrary pods to emphasize the effect.

### Deploy Nginx with Toleration and NodeSelector

Adding a matching Toleration to a pod specification will allow the pod to be scheduled on the nodes with a Taint. You can see this toleration below:

```
      tolerations:
      - key: dedicated
        operator: Equal
        value: advanced
        effect: NoSchedule
```
It should be noted that tolerations do not define attraction, merely permissions. In the scenario where you have provisioned special hardware for a workload, you may want to define attraction using nodeSelector or nodeAffinity.

[This](https://github.com/agmsb/k8s-scheduling-lab/blob/master/kubernetes/deployments/nginx-toleration-nodeselector.yaml) .yaml will add nodeSelector to the pod specification to also ensure that the permitted pod is scheduled on "advanced-pool" Node Pool. GKE provides us with OOTB labels in the nodeSpec; use the label signifying Node Pool name.

```
      nodeSelector: 
        cloud.google.com/gke-nodepool=dead-pool
```

Deploy the new nginx pod using a Deployment titled "nginx-toleration-nodeselector.yaml".

```
kubectl apply -f kubernetes/deployments/nginx-toleration-nodeselector.yaml
```

Now get the pod resource to see what node it was scheduled on.

```
kubectl get po -o wide 
```

This pod should now be running on a node in your "advanced-pool" Node Pool.

### Wrapping Up 

[Let's move on to Resource Quotas!](/resource_quotas.md)
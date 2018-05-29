## Resource Quotas Lab

### Understanding Namespaces

Namespaces are a core concept in Kubernetes. These provide us a way to represent multiple "virtual" clusters in a given Kubernetes cluster.

What this means is that most Kubernetes API Objects are scoped to a given Kubernetes Namespace. We also can define and govern policies at the namespace layer around access control and resource quotas. This lab will evaluate resource quotas in a Kubernetes Namespace.

### Creating a Namespace

We will start by observing the default namespaces Kubernets provides us:

```
kubectl get namespaces
```

You should see a default Namespace, a kube-public Namespace, and a kube-system Namespace.

Create your own Namespace.

```
kubectl create ns myspace
```

We now have our own "virtual" cluster in the Namespace titled "myspace".

### Creating a Resource Quota

Let us now apply a resource quota to the "myspace" Namespace. This quota will limit the number of pods in this Namespace to 1. Though a simplistic example, resource quotas are also available for other resources like CPU/Mem requests and limits.

```
kubectl apply -f kubernetes/resourcequotas/resourcequota-pods.yaml
```

We now have a resource quota of 1 Pod applied our "myspace" Namespace.

### Observing Resource Quota Effect

We can now create pods to test this Resource Quota. Begin by consuming the entire quota with a single pod.

```
kubectl apply -f kubernetes/pods/pod.yaml
```

Then try to exceed the given quota:

```
kubectl apply -f kubernetes/pods/pod-2.yaml
```

Our resource quota is now in effect.

### Wrapping Up

Let's move on to [validating admission webhooks](https://github.com/kelseyhightower/denyenv-validating-admission-webhook)!


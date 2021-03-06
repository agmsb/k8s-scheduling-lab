# Kubernetes Scheduling Lab

If you are reading this, welcome! We will be reviewing ways to influence scheduling in Kubernetes.

Also beware, this is definitely not an official Google product.

## Requirements

This lab currently assumes that you have the below set up:

1. Google Cloud Platform Project
2. gcloud SDK configured
3. Google Kubernetes Engine Cluster in a single GCP Zone
4. Have this repository cloned in your Google Cloud Shell.

Please note that there are respective billing costs associated with running resources in Google Cloud Platform.

## Expectations 

In this lab, we will evaluate influencing scheduling by doing the following:

[Taints and Tolerations Lab](/labs/taints_tolerations.md)

1. Add a Node Pool to our GKE cluster with Taints
2. Observe Taint Effect
3. Apply Toleration and NodeSelector to a given Workload
4. Observe Toleration and NodeSelector Effect

We will also complete the:

[Resource Quotas Lab](/labs/resource_quotas.md)

5. Create Resource Quotas in a Namespace
6. Observe Resource Quota Effect

Lastly, feel free to peruse [Kelsey Hightower's excellent tutorial](https://github.com/kelseyhightower/denyenv-validating-admission-webhook) on validating admission webhooks, where you will:

7. [Optional] Create a Validating Admission Webhook
8. [Optional] Observe Validating Admission Webhook Effect





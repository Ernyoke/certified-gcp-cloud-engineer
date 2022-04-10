# Containers

## Google Kubernetes (k8s) Engine (GKE)

- Kubernetes is an open-source orchestrator for containers for managing and scaling applications
- Kubernetes let's us deploy containers on a set of nodes called cluster
- A node represents a computing instance, in GC these are Compute Engine instances (virtual machines)
- GKE: is a Kubernetes as a managed service in the cloud
- Whenever k8s deploys an container or a number of related containers, it does so in a abstraction called as a pod
- Each pod in k8s gets an unique address
- Containers in pod can communicate with each other using localhost
- To expose the containers from a pod to the public internet, we can attach a load balancer to the cluster
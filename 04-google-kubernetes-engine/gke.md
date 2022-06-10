# GKE and Kubernetes Concepts

- Kubernetes is an orchestration platforms for containers
- It provides a platform to automate, schedule and run containers on physical and virtual machines
- Provides a framework to run distributed systems resiliently
- It works with a range of container tools, including Docker

## Google Kubernetes Engine (GKE)

- It is a managed Kubernetes Service provided by Google
- It has the benefits of advanced cluster management features with services like:
    - Cloud Load Balancing: spread the traffic between clusters and nodes
    - Node Pools: designate subnets of nodes within a cluster
    - Automatic scaling
    - Automatic updates
    - Node auto-repair
    - Logging and monitoring

## Cluster Architecture

- A cluster is the foundation of GKE
- In GKE a cluster consists of at least one control plane and one ore more worker nodes
- A control plane manages the state of the cluster and it insures that it is at the desired state
- The control plane is responsible for scheduling and management of nodes. It also managed network and storage resources of those workloads
- The control plane makes sure the cluster is in the desired state
- Nodes are compute engine VM instances create by GKE on our behalf
- Each node is managed from the control plane
- Nodes are responsible for running the Docker runtime

## Control Plane Components

- API server: all interactions with the cluster is done through API calls or kubectl
- kube scheduler: discovers and assigns newly created pods to appropriate nodes
- kube controller manager: runs all controller processes. It is responsible for things like noticing an responding when nodes go done, maintaining the correct number of pods, creating default account and access tokens, etc.
- cloud controller manager: runs controllers specific to the cloud providers
- etcd: key-value store that stores the state of the cluster

## Node Components

- kubelet: agent for communication with the control plane. It is responsible for starting and running docker containers in the specific nodes
- kube-proxy: maintains network connectivity to the pods
- runtime: software responsible for running containers (example Docker, containerd)

## GKE Cluster and Node Management

- Node Pools: 
    - Group of nodes within a cluster with the same configuration
    - It can contain one or multiple nodes
    - Custom node pools: useful for pods that require more resources
    - Any configuration changes affect the whole node pool
    - Any existing node pool can manually or automatically upgraded to the latest version of configurations
- GKE Cluster types:
    - Zonal Cluster:
        - They have a single control plane in a single nodes
        - Nodes can be distributed in a single zone (Single-zone) across multiple zones (Multi-zonal)
    - Regional Cluster:
        - Control planes are replicated across multiple regions
        - They consume more compute resources because of replication
    - Private Cluster:
        - Network traffic is isolated to the cluster only
        - For outbound connectivity we can use Cloud NAT or we can managed our own gateway
        - In private cluster the control planes VPC network is connected to our GKE VPC with VPC peering
        - The control for a private cluster has a private and a public endpoint as well. Public endpoint can be disabled
- Cluster Version: 
    - It is recommended to have auto-upgrade enabled for the cluster
    - If it is enabled we can chose between Release Channels. They can be the following:
        - Rapid: gets the latest k8s release as soon as possible
        - Regular (default): we get the latest k8s features 2-3 months after the Rapid release
        - Stable: changes are rolled last, after being validated 2-3 months in the Regular channel
    - Specific Version:
        - If we need a specific version of k8s, we can choose that the cluster creation
- Cluster Upgrades:
    - Control planes and nodes do not always run the same version at all times
    - A control plane is always upgraded before its nodes
    - In a zonal cluster we cannot launch or edit workloads during upgrade
    - With a regional cluster, each control plane is upgraded one by one
    - Auto-upgrade: is enabled by default (recommended best practice)
    - Manual upgrade: we cannot upgrade the control plane more than one minor version at a time
    - Maintenance windows and exclusions are available for any cluster upgrade
- Node and Node Pool Upgrade:
    - Auto-upgrade is enabled by default (best practice)
    - Manual upgrade is also available
    - Maintenance windows and exclusions are available
    - Pods scheduled to run on another node during upgrade
    - Upgrade is complete when:
        - All nodes have been recreated
        - Cluster is in the desired state
- Surge Upgrades:
    - We can control the number of nodes GKE can upgrade at a time
    - We can use surge upgrades to reduce disruption on a node pool. Also allows to control the number of nodes which are upgraded in parallel
    - Surge upgrades are determined by 2 settings:
        - `max-surge-upgrade`: number of additional nodes which can be added during an upgrade
        - `max-unavailable-upgrade`: number of nodes which can be simultaneously unavailable

## Pods and Object Management

- Kubernetes Objects are persistent entities, they represent the state of the cluster
- Almost every k8s object includes 2 nested object fields:
    - Object spec: hast to be set on creation, it represents a desired state
    - Object status: current state described by k8s
- Each object has a name and uuid. Only one object at a given time can have same name
- Objects are created and modified through a manifest file (YAML or JSON)
- Pods are the smallest, most basic deployable objects
- Pods contain one or more containers. In case of multiple containers, they are managed as single entity and they share the same pod resources (shared networking, shared storage)
- It is not recommended to create individual pods directly, instead we should create Replicas
- Namespaces: used for management purposes, multiple projects can share rhe same cluster by using namespaces
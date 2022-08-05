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
- Namespaces: 
    - Used for management purposes, multiple projects can share rhe same cluster by using namespaces
    - K8s starts with 4 initial namespaces: default, kube-system, kube-public, kube-node-lease
- Labels:
    - Key value pairs, which help to organize Kubernetes objects
    - Each object can have a set of key-value objects, each label must be unique for a object
- Pod lifecycle:
    - Pods are ephemeral
    - Terminated pods can not be brought back
    - Pods do not heal or repair themselves
    - Pods do not replace themselves
    - Pod lifecycle states:
        - Pending -> Running -> Succeeded
                             -> Failed
        - Unknown phase: can occur due to an error
- Replica sets:
    - Ensures that a specify number of pods running at any given time
    - Are managed by deployments, but they can be used by themselves as well

## Workloads

- Objects that set deployment rules for pods
- They let us define the rules for application scheduling, scaling and upgrading
- Type of workloads:
    - Deployments: run multiple replicas of an app and automatically replace any instances that fail
    - StatefulSets: used for apps that requires persistent storage
    - DaemonSets: ensures that every node in the cluster runs a copy of a pod
    - Jobs: used to run a finite task until completion
    - CronJob: similar to jobs, but run until completion on a schedule
    - ConfigMaps: configuration info for any workload to reference

## Kubernetes Services

- A service is an abstraction on top of logical selection of pods
- Provides a persistent IP address and a DNS name with which the pods can be accessed
- Allows for routing external traffic into the cluster
- It can used for routing inside the cluster. Can be used a load balancer for pods and for scaling these pods
- It automatically handles the recreation of pods
- In order for a service to route the traffic, the manifest file has to contain a name for DNS and a selector to define what pod should be included in the service
- Routing works by forwarding the network requests to certain pods which match the specified labels
- Service types:
    - `ClusterIP`: default k8s service
        - Gives a default service which can be accessed by other apps in the cluster
        - It is not exposed outside the cluster but it can be addressed from inside the cluster
        - It has a static IP address which can be used inside the cluster
        - The cloud SDK of CloudShell can be used to connect to this service form the outside
    - `NodePort`: it is a static port between 32000 - 32767
        - The value of the port can be randomly assigned by k8s or chosen by the user
        - The service can be accessed by `[NODE_IP]:[PORT]`
        - The service can be accessed from outside of the cluster
        - It is not secure since it opens up the whole cluster for outside access
        - It is an extension of the ClusterIP type
    - `LoadBalancer`: it is an internal k8s service which connects to a load balancer provided by the cloud provider
        - It is an extension of the NodePort type
        - The default method to expose a service
    - Multi-port Services: used to expose multiple ports for a service
    - `ExternalName`: provides an internal alias for an external DNS name
        - It is not associated with a set of pods or a DNS name
        - It is essentially a set of CNAME redirection
    - Headless service type: `serviceType: None`
        - Great use case for this is when no load balancing or routing is needed

## Ingres for GKE

- In GKE an ingress object defines rules for routing HTTP and HTTPS traffic to applications running in a cluster
- An ingress object is associated with on ro more service objects
- When we create an ingress object, GKE creates an HTTP load balancer and configures it according to the information in description
- The load balancer is given a stable IP address
- Ingress can be used to expose multiple services with a single load balancer

## Network Endpoint Groups (NEG)

- It is a config object which specifies a group of backend endpoints and services
- NEG are useful for container-native load balancing, where each container can be represented as an endpoint to a load balancer
- NEGs allow compute engine load balancers to communicate directly with pods

## Health Checks

- Default and inferred parameters are used if there are no specified health check parameters
- Should be explicitly defined by using a Backend Config custom resource definition (CRD) for the service

## SSL Certificates

- There are 3 ways to provide certificates to an HTTPS load balancer:
    - Google-managed:
        - Completely managed by Google
        - They do not support wildcard domains
    - Self-managed certificates:
        - We can provision our own certificates and create a certificate resource in the gcp project
        - We can then list the certificate in annotation for use
    - Self-managed as Secrets
        - Provisioned by us
        - We can create a secret to hold the certificate and refer this secret for use
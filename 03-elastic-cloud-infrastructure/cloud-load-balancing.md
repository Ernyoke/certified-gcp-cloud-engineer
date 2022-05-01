# Cloud Load Balancing

- Fully distributed, software defined managed service
- Using Cloud Load Balancing, we can serve content as close as possible to the end users
- It can respond to over 1 million queries per second
- GCP offers different types of load balancers:
    - Global:
        - HTTP(S)
        - SSL Proxy
        - TCP Proxy
    - Regional:
        - Internal TCP/UDP
        - Network TCP/UDP
        - Internal HTTP(S)
- Global Load Balancers are deployed on the point of presence locations globally
- Regional load balancers distribute traffic between resources in a region

## Managed Instance Groups

- A Managed Instance Group is a collection of identical VM instances that we control as a single entity with an instance template
- Managed instance groups can scale when there is demand for more compute power
- Managed instance groups can work with load balancing services to distribute traffic between instances within the group
- Managed instance groups can automatically identify a recreate unhealthy instances
- They are typically used with an autoscaler
- Regional managed instance groups are recommended over zonal instance groups
- In order to create a managed instance group, first we need to create an instance template
- The instance group managed automatically populates the instance group based on the template
- Autoscaling capabilities of a managed instance groups:
    - Automatically add/remove instances based on increase/decrease of load
    - Autoscaling policies can be defined based on:
        - CPU utilization
        - Load balancing capacity
        - Metrics
        - Queue-based workloads
- Managed instance group health checks:
    - Similar to uptime checks in Stackdriver
    - Used for determining if an instance is healthy based on periodical checks and thresholds

## HTTP(S) Load Balancing

- L7 load balancer
- Provides global load balancing for HTTP(S) requests
- Provides an anycast IP address for clients
- HTTP request are load balanced on port 80 or 8080, HTTPS request are load balanced on port 443
- Supports IPv4 and IPv6
- We can configure URL maps for routing requests to predefined resources based on URL of the request
- Backends service:
    - Offer health checks, session affinity (stickiness), time out setting and one or more backed
    - Backends contain:
        - An instance group (managed or unmanaged)
        - A balancing mode (CPU utilization or RPS - requests per second): how to determine when the backend is in full usage
        - A capacity scaler (ceiling % of CPU/Rate targets)
- HTTPS load balancer:
    - Uses a target HTTPS proxy
    - Requires at least on signed SSL certificate installed on the target HTTPS proxy (target proxy can have up to 15 SSL certificates)
    - Client SSL session terminates at the load balancer
    - Supports the QUIC transport layer protocol
- Backed bucket:
    - Allow us to use storage buckets with HTTPS load balancing
    - Common use case: send requests for dynamic data to a backend service, send requests for static data to a bucket
- Network endpoint groups (NEG):
    - Is a configuration object which specified a group of backend endpoints or services
    - NEGs can be:
        - Zonal: one ore more endpoints which can be Compute Engine VMs or services running on these VMs
        - Internet: single endpoint hosted outside of Google Cloud
        - Serverless: points to Cloud Run, App Engine services
        - Hybrid connectivity: points to traffic director services running outside of GC

## SSL Proxy Load Balancing

- Is a global load balancing service for encrypted non HTTPS traffic
- Terminates user SSL connection at the load balancing layer then balances the connection between the instances
- The instances can be in multiple regions, the traffic is redirected to the closes one
- Supports both IPv4 and IPv6
- Provided features:
    - Intelligent routing: can route requests to backend locations where is capacity
    - Certificate management
    - Security patching
    - SSL policies

## TCP Proxy Load Balancing

- Is a global load balancing service for un-encrypted non HTTP traffic
- Terminates connections at the load balancing layer and then forwards traffic to the closest backend
- Supports both IPv4 and IPv6
- Provided features:
    - Intelligent routing: can route requests to backend locations where is capacity
    - Security patching

## Network Load Balancing

- It is a regional, non-proxied load balancer
- It is using forwarding rules based on the incoming IP protocol data such as address, port and protocol traffic
- It can be used to load balance UDP, TCP/SSL traffic
- Architecture depends weather we use a backend service-based network load balancer or a target pool based network load balancer
- Backend service-based architecture:
    - Enables new feature which are not supported with legacy target pools such as:
        - Non-legacy health checks
        - Auto-scaling with managed instance groups
        - Connection draining
        - Configurable failover policy
    - Target pool load balancer can be transitioned to backend service-based lb
- Target pool-based architecture:
    - A target-pool resource defines a group of instances that receive incoming traffic from forwarding rules
    - The load balances picks an instance based on the hash of the source IP and port, and the destination of the source IP and port
    - Target pools can only be used with forwarding rules that can handle TCP and UDP traffic
    - Each target pool can have only 1 health check

## Internal Load Balancing

- It is a regional private load balancing service for TCP and UDP based traffic
- It is only accessible with internal IP addresses within a region
- The internal client requests are staying internal within Google's network
- Offers reduced latency (because of the internal traffic)
- Internal HTTP(S) load balancing:
    - Proxy based, regional, private load balancer
    - Layer 7 load balancer, can handle HTTP, HTTPS and HTTP/2 protocols
    - It is based on open source Envoy proxy
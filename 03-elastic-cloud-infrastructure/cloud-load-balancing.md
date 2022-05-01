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
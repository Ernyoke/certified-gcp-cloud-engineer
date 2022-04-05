# Compute

## Virtual Private Cloud (VPC)

- Each VPC network is contained in a GCP project
- VPCs have global scope. They can have subnets in any GCP region worldwide
- Subnets can span the zone that make-up a region
- We can have resources in different zones in the same subnet
- We can dynamically increase the size of a subnet

## Compute Engine

- Let's us create and run virtual machine instances in the cloud
- When a machine is created, we can pick a machine type (determines memory and CPU)
- If there is no predefined type for our use-cases, we can make a custom VM
- VMs can have dedicated GPUs
- We can pick persistent disks for storage. We can chose standard or SSD storage types
- We can attach a local SSD for higher performance. Data is not persisted if the VM is terminated
- Preemptible VMs: they can be terminated by GCP if their resources is needed elsewhere. They are recommended for saving costs

## VPC Capabilities

- VPCs have route tables for managing network connectivity routing
- VPCs have a global distributed firewall
- We can define firewall rules as metadata tags on the compute engine instances
- VPC Peering: connect VPCs between projects
- Cloud Load Balancing: fully distributed, software defined managed service for all the traffic. We don't have to manage and scale them
- Cloud Load Balancers support HTTP, HTTPS, other TCP and SSL traffic and UDP traffic
- With Cloud Load Balancing a single unicast IP fronts the whole backend
- Load-balancing options:
    - Global HTTP(s): L7, can route different URLs to different backends
    - Global SSL Proxy: L4, can load-balance non-HTTPS SSL traffic supported on specific ports
    - Global TCP Proxy: L4 lb for non-SSL TCP traffic
    - Regional: load-balancing of any traffic (TCP, UDP) on specific ports
    - Regional Internal: load-balancing of traffic inside a VPC
- Cloud DNS: managed, highly available and scalable DNS service
- Cloud CDN (Content Delivery Network): we can use Google's globally distributed edge caches to cache content close the users
- Cloud Router: allows for on-premises networks and Google VPCs to change routes over VPN using BGP
- Direct Peering: offers private connection between on-premises and Google for hybrid solutions
- Carrier Peering: hybrid connectivity through Google partners
- Dedicated Interconnect: we can connect N * 10G transport circuits for private cloud traffic to GCP. Offers 99.99 SLA
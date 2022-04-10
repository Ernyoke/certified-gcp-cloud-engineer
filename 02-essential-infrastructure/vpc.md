# VPC - Virtual Private Cloud

- Projects are the key organizer of infrastructure resources in Google Cloud
- The default quota for each project is 5 networks
- Networks can be shared or peered with other networks
- These networks do not have IP ranges. Google Cloud networks are global and span across all available regions
- Inside networks we can segregate resources in subnetworks
- There are 3 types of networks:
    - Default: every project is provided with a default network. This network has a subnet in each region with non-overlapping CIDR ranges and default firewall rules (SSH, RDP, ICMP from anywhere and egress traffic to anywhere)
    - Auto: one subnet for each region is automatically created in it. These subnets usa a /20 mask which can be expanded up to a /16 mask. All this subnets fit in the 10.0.0.0/9 CIDR block. If new region become available, new subnets are added to the network
    - Custom: does not automatically create subnets. We are fully in control about the IP ranges for the subnets, region where they are created
- An auto-mod network can be converted to custom, but not vice-versa
- Subnets works at a regional scale. Subnets can cross zones
- Subnets are assigned an IP range. The first and second addresses from the range are reserved for the network and subnet gateway
- Other reserved addresses are the second to last and the last addresses (broadcast IP addresses)
- Subnets can be extended without any downtime. They cannot shrink
- In case of extension the new subnet mask should not overlap with any other subnet range from the network
- Auto mode subnets can be extended from /20 to /16

## IP Addresses

- In GCP each VM can have 2 IP addresses:
    - An internal IP address allocated by DHCP. Any VM or any service which depends on an IP address (example App Engine, GKE) gets this internal IP address
    - External IP address (optional): we can address this IP address if the service requires it. We can assign this IP address from a pool or from a reserved ip address (static). If we have allocate a static IP address and not assign it to a machine, we are charged for it
- We can use our publicly routable IP addresses with bringing into GPC a /24 IP block or larger (BYOIP)

## DNS Resolution for Internal Addresses

- Each instance has a hostname that can be resolved to an internal IP address:
    - The hostname is the same as the instance name
    - FQDN is `[hostname].[zone].c.[project-id].internal`
- Name resolution is handled by internal DNS resolver:
    - Provided as part of the Compute Engine (`169.254.169.254`)
    - Configured for use on instance via DHCP
    - Provides answers for internal and external addresses

## DNS Resolution for external Addresses

- Instances with external IP address connections from hosts outside the project
- DNS records for external addresses can be published using existing DNS servers (outside of Google Cloud)
- DNS zones can be hosted using Cloud DNS

## Cloud DNS

- It a scalable, reliable, managed authoritative domain name system (DNS service)
- It is using Google's global network of anycast nameservers to serve DNS zones
- GCP offers an 100% update SLA for Cloud DNS
- Cloud DNS allows creation and update of million DNS records without the burden of managing own DNS servers

## Alias IP Ranges

- Allows us to assign a range of IP addresses as aliases to a VM's network interface
- Useful if want to assign multiple IP addresses to VM in case we are running multiple applications on it (example: containers)

## Routes and Firewalls

- By default every network has:
    - Routes that let instances in a network send traffic directly to each other
    - A default route that directs packets to destinations tha are outside of the network
- The default network firewall rules configured to allow instances ona network talk to each other. Manually created networks do not have such rules
- Instance routing tables:
    - Each route in the routes collection may apply to one or more instances
    - A route applies to an instance if the network and the instance tag match with the rule
    - If there are no tags specified for the rule, it will apply to all the instances from the network
- GCP firewall rules protect our VM instances form unapproved connections
- GCP firewall rules are stateful
- Firewall rule properties:
    - direction: ingress or egress rules
    - source or destination
    - protocol and port
    - action: allow or deny packets that match the direction, protocol, port and source destination of the rule
    - priority
    - Rule assignment: all rules are assigned to all instances, but we can assign certain rules to certain instances only

## Network Pricing

- Ingress traffic is free (responses to requests are considered egress traffic which is charged)
- Egress traffic to the same zone (internal IP address) is free
- Egress traffic to Google products (Youtube, Maps, Drive) is free
- Egress traffic to GCP services within the same region is free, with some exceptions
- Egress traffic to the same same region: $0.01/GB
- Egress traffic to the same zone using external IP address: $0.01/GB
- Egress traffic between regions in the US and Canada: $0.01/GB
- Egress traffic between regions outside of US: varies by region
- Price of static IP addresses (assigned but not used): $0.01 per hour
- Static and ephemeral IP addresses in use on standard VM: $0.004 per hour
- Static and ephemeral IP addresses in use on preemptible VM: $0.002 per hour
- Static adn ephemeral IP addresses attached to forwarding rules are free of charge
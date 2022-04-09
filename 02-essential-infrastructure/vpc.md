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
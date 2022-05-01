# Shared VPC and VPC Peering

## Shared VPC

- Allows an organization to connect resources from multiple projects to a common VPC network
- Allows the resources to communicate using internal IPs from the shared network

## VPC Peering

- Allows private connectivity across VPC networks regardless if they belong to the same project or same organization
- Each VPC network may have its own firewall rules
- In order for VPC peering to be established the producer network admin needs to peer the producer network with the consumer network and vice-versa
- When both peering connections are created, the peering session becomes active and routes are exchanged
# Cloud Interconnect

- Cloud Interconnect ans Peering services available in GCP:

|         | Dedicated              | Shared               |
|---------|------------------------|----------------------|
| Layer 3 | Direct Peering         | Carrier Peering      |
| Layer 2 | Dedicated Interconnect | Partner Interconnect |

## Dedicated Interconnect

- Provides direct physical connections between on-premises networks and Google's networks
- Enables transfer of large amount of data between on-premises and GCP
- For using it we nee to provision a Cross Connect between on-premises router and Google Network in a common colocation facility
- Dedicated Interconnect can be configured to provide a 99.9% or 99.999% SLA
- In order to use Dedicated Interconnect, our own network has to physically meet Google's network in a supported colocation facility

## Partner Interconnect

- Provides connectivity between on-premises network and Google network through a supported service provider
- Recommended if our facility is geographically far away from a colocation facility or if our data transfer requirements don't warrant a Dedicated Interconnect
- Service provider has physical connectivity to GCP which is provided as a service to customers

## Comparison of Interconnect options

- IPsec VPN tunnel:
    - Encrypted tunnel to VPC through the public internet
    - 1.5 - 3 Gbps per tunnel
- Dedicated Interconnect:
    - Dedicated, direct connections to VPC networks
    - 10 Gbps per link or 100 Gbps
- Partner Interconnect:
    - Dedicated bandwidth connections to VPC network through a service provider
    - 50 Mbps - 10 Gbps per connection

## Direct Peering

- Provides a direct connection between our business network and Google's network
- With this connection we are able to exchange traffic using one the Google's broad-reaching edge network location
- Direct Peering is done by exchanged BGP routes between Google and peering entity
- After the connection is in place, Direct Peering can be used to reach all the Google services and GCP products
- Direct Peering does not have an SLA

## Carrier Peering

- Provides connectivity similar to Direct Peering through a supported partner
- Carrier Peering does not have an SLA

## Comparison between Direct and Carrier Peering

- Direct Peering:
    - Dedicated, direct connection to Google's network
    - Capacity of 10 Gbps
- Carrier Peering:
    - Peering through a service provider to Google's public network
    - Varies based on partner offering

## Choosing a Connection

- L2 (interconnect) vs L3 (peering)
- Interconnect services:
    - Provide direct access to RFC1918 IPs in our VPC with SLA
- Peering services:
    - Access to Google public IPs only without SLA
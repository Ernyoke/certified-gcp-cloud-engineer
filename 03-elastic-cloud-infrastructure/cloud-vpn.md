# Cloud VPN

- Security connects on-premises network to the GCP VPC network
- Traffic traveling between the two network is encrypted
- Useful for low-volume data connections
- Provides 99.9% SLA and supports the following:
    - Site-to-site VPN
    - Static routes
    - Dynamic routes via Cloud Router
    - IKEv1 and IKEv2 ciphers
- Cloud VPN is a regional resource using a regional IP address
- For having a connection between the VPC and on-premises network, Cloud VPN requires a tunnel between a Cloud VPN Gateway and an On-premises VPN Gateway
- MTU can not be greater than 1460 bytes (because encryption)
- Cloud Router:
    - Required for dynamic router
    - Uses BGP for exchanging routes
    - To setup BGP, 2 additional IP addresses are required on each end. These IP addresses must be link-local belonging to the IP range of `169.254.0.0/16`. These IP addresses are not part of both local networks, they are exclusively used to establish BGP sessions
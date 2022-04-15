# Compute Engine

- Infrastructure as a Service (IaaS)
- Offers predefined or custom virtual machine types. We can chose the:
    - vCPU (cores) and Memory (RAM)
    - Storage:
        - Zonal or regional persistent HDD or SSD
        - Local SSD
        - Cloud Storage
    - Networking
    - OS: Linux or Windows
- A vCPU is equal to 1 hardware hyper-thread. The CPU will affect the network throughput (2GBits/sec for each vCPU core - except for instances with 2 or 4 vCPU where we receive 10GBit/sec bandwidth)
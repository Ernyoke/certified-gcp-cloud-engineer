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
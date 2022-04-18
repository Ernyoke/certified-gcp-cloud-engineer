# Databases

## Cloud SQL

- It is a fully managed service of either MySQL, PostgreSQL or Microsoft SQL server
- Patches and updates are automatically applied
- We still have to manage and administer users for these databases
- Cloud SQL supports many clients:
    - `gcloud sql`
    - App Engine, Google Workspace scripts
    - Applications and tools:
        - SQL Workbench, Toad
        - External applications using standard MySQL drivers
- Cloud SQL high performance and scalability:
    - Up to 64 TB of storage
    - Up to 60_000 IOPS
    - Up to 624 GB or RAM per instance
    - Ability to scale out with read replicas
- Other Cloud SQL services:
    - HA configuration: primary-standby instances with synchronous replications
    - Backup service: automated and on-demand backups
    - Import/export
    - Scaling: up (change machine capacity), out (read replicas)
- Connecting to a Cloud SQL instance:
    - Same project in the same region: chose private IP connection for most performance and most secure
    - Other region, or from outside of GCP:
        - Recommended: use Cloud SQL proxy (offers key rotation)
        - Manual SSL connection
        - Connect from authorized network (if no SSL connection is available)
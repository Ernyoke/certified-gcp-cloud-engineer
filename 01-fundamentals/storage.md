# Storage

## Cloud Storage

- Provides object storage
- Object storage: key-value pairing between a unique string keys and binary data stored in the cloud
- Cloud Storage is a fully managed, scalable service. We don't need to provision capacity ahead of time
- Can be used for: serving website, storing archives, distributing large storage of data to the end-users
- Cloud Storage is not a file system
- It is comprised of buckets
- Objects are immutable, we create new versions when edition a file
- Control access to objects and buckets: we can use IAM or Access Control Lists for finer controls
- Cloud Storage object versioning: used to keep a history of changes on an object. Can be enabled/disabled in case of a bucket
- Lifecycle management policies: Cloud Storage can apply actions on objects based on policies (example: delete files older than 3 months)
- Storage classes:
    - Multi-regional: high performance object storage, it is geo-redundant storage, data is stored in at least two regions which are geographically separated by at least 140 km, Availability SLA: 99.95%
    - Regional: high performance object storage, let's us storage in a bucket in a specific region. It is cheaper than multi-regional storage, but it offers less redundance. SLA: Availability 99.9% 
    - Nearline: backup object storage, used for storing infrequently accessed data. It is better suited for scenarios when data is read/modified once a month or less. Availability SLA: 99.00%
    - Coldline: backup object storage, very low cost storage recommended for data archiving, online backup and disaster recovery. It is the best choice for data planned to access at most once per year. It has a 90 day minimum storage duration. I has cost per data access and higher per operation cost on data. Availability SLA: 99.00%
- Storage price is based on the size of data, multi-regional storage class has the highest cost, while coldline class offers the lowest cost
- Nearline storage includes an access free for GB per data read, Coldline storage incurres a higher fee for GB per data read
- Bring data into the cloud:
    - Online transfer: gsutil tool, upload and access dat from the command line
    - Storage Transfer Service: lets manage scheduled batch data imports for other cloud services, from a different region or from a HTTPS endpoint
    - Transfer Appliance:
# Cloud Storage

- It is Google Cloud's object storage service
- It allows worldwide storage and retrieval of any amount of data at any amount of time
- Can be used for data distribution, backups, recovery, etc.
- It scales to exabytes of data
- The time to the first byte is in milliseconds
- It offers high availability across all storage classes
- It offers a single API across all storage classes
- Cloud Storage is collection of buckets. Data in directories is stored as key-value pairs
- It has 4 storage classes:
    - Standard: hot data, most expensive storage class. It has no data retrieval cost and minimum storage time
    - Nearline: low cost, highly durable for storing infrequently accessed data
    - Coldline: very low cost, for storing infrequently accessed data. Require a minimum of 90 day storage of data
    - Archive: lowest cost for data archiving, online backups and DR. Data is available in milliseconds. It has no availability SLA. It has the highest cost for data access and management, and a 365 minimum storage duration
- Each of these storage classes offers 3 location types:
    - Multi-region
    - Dual-region
    - Region
- Objects stored in multi-region and dual-region are redundant
- All data classes offer "eleven nines" of durability SLA (essentially no data loss)
- Cloud Storage is brocken down to the following components:
    - Buckets: the cannot be nested. Each bucket requires a globally unique name
    - Objects: no minimum size. They inherit the storage class of the bucket
    - Data access:
        - `gsutil` command line
        - JSON or XML APIs

## Changing Default Storage Classes

- When an object is uploaded, the default class is applied to the object, unless a storage class is specified
- The default storage class of a bucket can be changed
- The default storage class of an object can be changed as well
- Objects can be moved from bucket to bucket

## Access Control

- IAM roles and permissions
- ACLs: Access Control Lists
- Signed URL: timed access to a bucket or object
- Signed Policy Document
- ACLs: 
    - A mechanism of defining who has access to objects and what actions can it perform
    - Maximum number of ACLs per object is 100
    - An ACL contain a Scope (who) and a Permissions (what)
- Signed URLs:
    - For some application it is easier and more efficient to grant timed access to an object
    - Generate signed url:

    ```
    gsutil signurl -d 10 m <path-to-private-key> gs://bucket/object 
    ```

## Cloud Storage Features

- Customer-supplied encryption keys (CSEK)
- Object Lifecycle Management for automatically deleting or archiving objects
- Object versioning
- Directory synchronization: sync a VM with a bucket
- Object change notification
- Data import
- Strong consistency

## Object Versioning

- Objects are immutable
- With versioning we can maintain a history of modifications of an object
- We can list archived versions of an object, restore an object to an older state or delete a specific version
- Versioning can be turned on or off

## Lifecycle Management Policies

- They specify actions to be performed on objects that meet certain rules
- Examples:
    - Downgrade storage class on objects older than a year
    - Delete objects created before specific date
    - Keep only the most 3 recent versions of an object
- Object inspection occurs in async batches
- Changes can take up to 24 hours to be applied

 ## Object Change Notification

- Can be used to notify an application when an object is updated or added to a bucket
- Recommended: use Pub/Sub Notifications for Cloud Storage changes

## Data Import Services

- Transfer Appliance: hardware appliance, rack, used to migrate large amount of data. Transfer appliances are shipped to Google Cloud with data on it from on-premises
- Storage Transfer Service: import online data from another bucket or other source
- Offline Media Import: third-party provider uploads the data from a physical media

## Cloud Storage Consistency

- Cloud Storage offers strong global consistency for:
    - Read-after-write
    - Read-after-metadata-update
    - Read-after-delete
    - Bucket listing
    - Object listing

 ## Choosing Storage Class:

 - Archive storage: read data less than once per year
 - Coldline storage: read data less than once per 90 days
 - Nearline storage: read data less than once per 30 days
 - Standard storage: hot data
 - Location type:
    - Single region for optimizing latency and bandwidth within a region
    - Dual-region: similar performance for both regions, high availability and geo-redundancy
    - Multi-region: distribute data globally or high availability and geo-redundancy
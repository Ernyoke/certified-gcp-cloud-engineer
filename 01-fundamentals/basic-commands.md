# Basic CLI Commands

(Based on: https://pistocop.netlify.app/posts/ace_google_exam_notes/)

## gcloud Init

```
gcloud init
```

## gcloud Structure

```
$ gcloud compute instances  list
# |------base--| |--who--| |-what-|

$ gcloud components install  kubectl # exception
# |------base-----| |-what-| |-who-|
```

## Set the Project

```
gcloud config set project PROJECT-NAME
```

## Bucket Versioning (NB: is gsutil)

```
gsutil versioning set (on|off) gs://<bucket_name>...
gsutil versioning get gs://<bucket_name>...

```

## List VM

```
gcloud compute instances list [--zones] [--format json]
```

## Start and Stopping VM Instances

```
gcloud compute instances start INSTANCE_NAMES
gcloud compute instances stop  INSTANCE_NAMES
```

## Create VM with Boot Disk

```
gcloud compute instances create VM_NAME \
    --source-snapshot=BOOT_SNAPSHOT_NAME \
    --boot-disk-size=BOOT_DISK_SIZE \
    --boot-disk-type=BOOT_DISK_TYPE \
    --boot-disk-device-name=BOOT_DISK_NAME
```

## Install Components (e.g. kubectl, minikube, kustomize, bq)

```
gcloud components list
gcloud components install PRODUCT
```

## Set a Default Region

```
gcloud config set compute/region europe-west1
```

## Create Compute Engine Persistent Disks

```
gcloud compute disks create my-disk-1 my-disk-2 --zone=us-east1-a
```

## Create a Snapshot of an Instance's Disk

```
gcloud compute disks snapshot DISK_NAME --snapshot-names=NAME
```

## Get K8s Cluster Credentials

```
gcloud container clusters get-credentials --zone us-central1-a standard-cluster-1
```

## Resize a Cluster Nodes

```
gcloud container clusters resize sample-cluster --num-nodes=2
```

## Add IAM Policy Binding

```
gcloud projects add-iam-policy-binding example-project-id-1  --member='user:test-user@gmail.com' --role='roles/editor'
```

## Delete `default` VPC (NB: start with 'compute')

```
gcloud compute networks delete default
```

## Create VPC

```
gcloud compute networks create
```

## gcloud Wide Flags

```
--account         # GCP user account to use for invocation
--project         # The Google Cloud Platform project ID to use for this invocation
--billing-project # project that will be charged quota for operations performed
--configuration   # The configuration to use for this command invocation
--flags-file      # A YAML or JSON file that specifies a --flag:value dictionary
--flatten         # Use to "flatten" resources list
--format          # Set the format for printing command output resources
--log-http        # Log all HTTP server requests and responses to stderr
--trace-token     # Token used to route traces of service requests for investigation of issues
--verbosity
--quiet
--impersonate-service-account
--zone
```

## List VPC networks

```
gcloud compute networks list
```

## List Existing Clusters for Running Containers

```
gcloud container clusters list
```

## Describe Cluster Image Info (NB: is gcloud not kubectl)

```
gcloud container images describe gcr.io/myproject/myimage:tag
```

## Kubernetes List Nodes, Pods

```
kubectl get nodes
kubectl get pods
```

## Kubernetes Get More Info about Nodes, Pods, Deployments, etc.

```
kubectl describe nodes
kubectl describe pods
kubectl describe deployments
```

## Connect to a SQL Database

```
gcloud sql connect db-mysql –user=root
```

## Create a Bucket for a SQL Database

```
gcloud sql backups create ––async ––instance [INSTANCE_NAME]
```

## Enable SQL Automatic Backups

```
gcloud sql instances patch [INSTANCE_NAME] –backup-start-time [HH:MM]
```

## Big Query Estimate Costs for a Query

```
bq ––location=[LOCATION] query ––dry_run [SQL_QUERY]
```
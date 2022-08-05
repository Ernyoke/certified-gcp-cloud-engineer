# Cloud Run

- Cloud Run is a managed compute platform that lets us run containers directly on top of Google's scalable infrastructure
- On Cloud Run, we code can either run continuously as a service or as a job. Both services and jobs run in the same environment and can use the same integrations with other services on Google Cloud:
    - **Cloud Run services**: used to run code that responds to web requests, or events
    - **Cloud Run jobs**: used to run code that performs work (a job) and quits when the work is done

## Cloud Run Pricing

- Scale to zero is attractive for economic reasons since we are charged for the CPU and memory allocated to a container instance with a granularity of 100ms
- If we don't configure minimum instances, we're not charged if your service is not used
- There are two pricing models you can enable:
    - Request-based: if a container instance is not processing requests, the CPU is not allocated and we're not charged. Additionally, we pay a per-request fee
    - Instance-based: we're charged for the entire lifetime of a container instance and the CPU is always allocated. There's no per-request fee

## Cloud Run Configurations

### Environment Variables for Services

- `PORT`: the port our HTTP server should listen on
- `K_SERVICE`: the name of the Cloud Run service being run
- `K_REVISION`: the name of the Cloud Run revision being run
- `K_CONFIGURATION`: the name of the Cloud Run configuration that created the revision
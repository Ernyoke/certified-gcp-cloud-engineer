# App Engine

- App Engine is a PaaS (Platform-as-a-Service) offering
- The App Engine service managed the hardware and the networking infrastructure
- App Engine provides built-in services that many web-application need, such as NoSQL databases, in-memory caching, logging, health checks, load balances, etc.
- We only pay for resources that we use, App Engine is recommended for application where load is highly variable

## App Engine Standard Environment

- Offers a simple deployment experience compare to the Flexible Environment
- Offers fined-grained autoscaling
- Offers free daily usage quota (low usage service may run at no charge)
- Google provides several SDKs for development and deployment on AppEngine. We can test the application locally before uploading it to the AppEngine Service
- AppEngine runtimes: specific versions of Java, PHP, Python and Go
- For other languages we may want to consider the Flexible Environment
- Sandbox: software construct independent of the hardware. Constraints:
    - No writing to local files
    - All requests time out at 60 seconds
    - Limits in third-party software

## App Engine Flexible Environment

- Instead of the sandbox, we can specify the contain the App Engine is running on
- App Engine manages the containers, we get to chose where they are running
- App Engine applications can access GC services such as data stores, memory caches, task queues, etc.

## App Engine Standard vs Flexible Comparison

|                            | App Engine Standard                                                   | App Engine Flexible         |
|----------------------------|-----------------------------------------------------------------------|-----------------------------|
| Instance startup           | Milliseconds                                                          | Minutes                     |
| SSH access                 | No                                                                    | Yes (not by default)        |
| Write to local disk        | No                                                                    | Yes (ephemeral writes only) |
| Support 3rd party binaries | No                                                                    | Yes                         |
| Network Access             | Via App Engine services                                               | Yes                         |
| Pricing Model              | After free daily use, pay per instance class, with automatic shutdown | Pay for resource allocation per hour, no automatic shutdown |
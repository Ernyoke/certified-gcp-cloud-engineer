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

|                            | App Engine Standard                                                   | App Engine Flexible                                         |
|----------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------|
| Instance startup           | Milliseconds                                                          | Minutes                                                     |
| SSH access                 | No                                                                    | Yes (not by default)                                        |
| Write to local disk        | No                                                                    | Yes (ephemeral writes only)                                 |
| Support 3rd party binaries | No                                                                    | Yes                                                         |
| Network Access             | Via App Engine services                                               | Yes                                                         |
| Pricing Model              | After free daily use, pay per instance class, with automatic shutdown | Pay for resource allocation per hour, no automatic shutdown |

## App Engine Config Files

- `app.yaml`: defines our configuration settings for our runtime as well as general app, network, and other resource settings
- `cron.yaml`: a cron.yaml file should in the root directory of your application (alongside app.yaml) and configures scheduled tasks for our applications
- `dispatch.yaml`:  allows us to override routing rules. We can use the dispatch.yaml to send incoming requests to a specific service (formerly known as modules) based on the path or hostname in the URL
- `index.yaml`: we can use Firestore in Datastore mode (Datastore) for storing data for our applications that run in the flexible environment. We define indexes our app needs in a index.yaml configuration file

## App Engine IAM Roles

- App Engine Admin (`roles/appengine.appAdmin`):
    - Read/Write/Modify access to all application configuration and settings
    - To deploy new versions, a principal must have the Service Account User (roles/iam.serviceAccountUser) role on the App Engine default service account, and the Cloud Build Editor (roles/cloudbuild.builds.editor) and Cloud Storage Object Admin (roles/storage.objectAdmin) roles on the project
- App Engine Creator (`roles/appengine.appCreator`):
    - Ability to create the App Engine resource for the project
- App Engine Viewer (`roles/appengine.appViewer`):
    - Read-only access to all application configuration and settings
- App Engine Code Viewer (`roles/appengine.codeViewer`):
    - Read-only access to all application configuration, settings, and deployed source code
- App Engine Deployer (`roles/appengine.deployer`):
    - Read-only access to all application configuration and settings
    - To deploy new versions, you must also have the Service Account User (roles/iam.serviceAccountUser) role on the App Engine default service account, and the Cloud Build Editor (roles/cloudbuild.builds.editor) and Cloud Storage Object Admin (roles/storage.objectAdmin) roles on the project
    - Cannot modify existing versions other than deleting versions that are not receiving traffic
- App Engine Service Admin (`roles/appengine.serviceAdmin`):
    - Read-only access to all application configuration and settings
    - Write access to module-level and version-level settings. Cannot deploy a new version
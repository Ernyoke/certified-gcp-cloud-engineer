# Monitoring

## Stackdriver

- Dynamically discovers cloud resources and application services
- We can have deep visibility into our applications in minutes
- Provides us access to powerful data an analytics tools
- Stackdriver offers services for:
    - Monitoring
    - Logging
    - Error Reporting
    - Tracing
    - Debugging
- Supports several third party integrations

## Stackdriver Monitoring

- Is at the base os SRE
- It dynamically configures monitoring after resources are deployed
- Allows us to monitor platform, systems an application metrics
- Workspace:
    - Is a root entity that holds monitoring and configuration information in Stackdriver Monitoring
    - We can have as many workspaces as we want, GCP projects can't be monitored by more than one workspace
    - The first monitored project is the Hosting Project and needs to be specified at the workspace creation
- Stackdriver allows us to create custom dashboards and charts based on the monitored data
- Alerting policies: we can create alerting policies based on monitored data. We can create notifications based on these alerting policies
- Update checks: test the availability of the public services
- Monitoring agent: used to access system resources and application services. It can be installed in compute resources and application services

## Stackdriver Logging

- Allows us to store, search, analyze and alert on log data on events from GCP and AWS
- Logging includes storage for logs, an user interface Logs Viewer and an API to manage logs programmatically
- Logs are retained for 30 days, we can export logs into Cloud Storage, BigQuery and Cloud Pub/Sub
- Logging Agent: can be installed on VM instances for gathering logs

## Stackdriver Error Reporting

- Counts, analyzes and aggregates errors for running cloud services
- Provides a centralized error management interface

## Stackdriver Trace

- It is a distributed tracing system that collects latency data from application systems and generates in-depth latency reports
- Can collect data from App Engine, Google HTTP(S) load balances and applications implementing Cloud Trace SDKs

## Stackdriver Debugger

- Let's us inspect the state of a running application in real-time without stopping it or slowing it down significantly
- It can capture debug snapshots, call stack and local variables of a running application
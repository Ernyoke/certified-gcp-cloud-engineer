# Resource Management

## Resource Manager

- It let's us hierarchically manage resource by project, folder and organization
- Resource consumption is measured in quantities, like rate of use, time, number of items, feature use
- Each project is associated with one billing account
- A project accumulates the consumption of all of its resources. It can be used to track resources and quota usage
- Resources can be categorized as:
    - Global: images, snapshots, networks
    - Regional: external IP addresses
    - Zonal: instances, disks

## Quotas

- All resources al subject to project quotas or limits
- Example of quotas:
    - How many resources can we create per project (15 VPCs per project)
    - How quickly we can make API requests (5 administrative access per project)
    - Regional quotas (24 CPUs region/project by default)
- If we expect an upcoming increased usage of resources, we can ask for quota increase in cloud console or by creating a support ticket
- Why do quotas exists:
    - Prevent runaway consumption in case of an error or malicious attack
    - Prevent billing spikes or surprises
    - Forces sizing consideration and periodic review

## Labels

- Are a utility for organizing gcp resources
- They are key-value pairs which can be attached to resources such as VMs, disks, snapshots, etc.
- Each resource can have up to 64 labels
- We can use labels for search resources, cost accounting or budgeting
- Labels are not tags:
    - Labels are user defined string propagated through billings
    - Tags are user defined strings applied to instances only, primary used for networking (applying firewall rules)

## Billing

- Billing is set up at the project level, when we set up a project, a billing account is linked to it
- Billing accounts can be linked to one or more projects
- Projects without a billing account can only use free gcp services
- Billing account can be charged monthly or at a set threshold
- Subaccounts can be used for separate billing for projects
- Budget:
    - Budgets can be set at the project level
    - To help with project planning and controlling costs we can set a budget
    - When we exceed a budget limit, we can configure our billing account to send an alert. We can set up a webhook as well for automation
- Budget Alerts: 
    - Alerts sent to billing admins after spending exceeds a budget percentage or a specified amount
    - In addition to email, we can use Pub/Sub to programmatically listen to budget alerts
- Reports:
    - We can export and query cost and spending information into BigQuery. We can visualize this data using Data Studio
- Quotas:
    - Designed to prevent over-consuming of resources because of an error or malicious attack
    - They do apply a the level o project
    - We have 2 types of quotas:
        - Rate quota: reset after a period of time
        - Allocation quota: do not reset at interval, we have to free up resources of adhere to these quotas. These quotas can be increased after requesting
    - Some quotas are fixed to all customers
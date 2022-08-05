# Cloud IAM

## Identity Access Management

- It is a way of identifying who can do what on each resource
- Example: read only access to get and read read-only resources

## IAM Resource Hierarchy

- Organization: represents our company
    - Folder: could represent a department, permissions assigned to folders are inherited by all resources the folder contains
        - Projects: represent trust boundary in the company
            - Resources

## Organization Node

- Root node of the IAM hierarchy
- Organization roles:
    - Organization Admin: control over all cloud resources, useful for auditing
    - Project creator: controls project creation, control over who can create projects
- Organization resource is closely associated with G Suite or Cloud Identity account
- When an user with a G Suite or Cloud Identity account creates GCP project an organization resource is automatically provisioned to them
- Workspace or Cloud Identity super administrator responsibilities are:
    - Assign the Organization admin role to some users
    - Point of contact in case of recovery issues
    - Control the lifecycle of the Workspace or Cloud Identity account and Organization resource
- Organization admin responsibilities:
    - Define IAM roles
    - Determine the structure of the resource hierarchy
    - Delegate responsibilities over critical components such as Networking, Billing and Resource Hierarchy through IAM roles
- Folders:
    - Provide additional grouping mechanism and isolation boundaries between projects (example: departments)
    - Folders allow delegation of administration rights
    - Folders can contain projects and other projects

## Resource Manager Roles

- Organization:
    - Admin
    - Viewer
- Folder:
    - Admin
    - Creator: browser hierarchy and create folders
    - Viewer: view folders and projects bellow a resource
- Project:
    - Creator: create new projects (automatic owner) and migrate new projects into the organization
    - Deleter: delete projects

## Roles

- There are 3 types of roles:
    - Basic roles: fixed, coarse grained level of access
        - Example of basic roles:
            - Owner:
                - Invite members
                - Remove members
                - Delete projects
                - All Editor and Viewer permissions
            - Editor:
                - Deploy applications
                - Modify code
                - Configure services
                - All Viewer permissions
            - Viewer:
                - Read-only access
            - Billing Administrator:
                - Manage billing
                - Add/remove administrators
    - IAM predefined roles:
        - Roles that apply to a predefined GCP service in a project
        - Collection of permissions, example `InstanceAdmin` role providing all the compute permissions
        - Examples of predefined roles:
            - Compute Admin: full control of compute engine resource
            - Network Admin: permissions to create, modify and delete networking resources, except for firewall rules and SSL certificates
            - Storage Admin: permissions to create, modify and delete disks, images and snapshots
    - Custom roles:
        - Let us define a precise set of permissions

## Members

- There are 5 different types of members:
    - Google Accounts: human users
    - Service Accounts: accounts for services
    - Google Groups: named collection of google accounts and service accounts
    - Google Workspace domain: virtual group of all the Google accounts created in an organization's workspace accounts
    - Cloud Identity: customers who are not workspace customers

## IAM policies

- A policy consists of a list of bindings
- A binding binds a lost of members to a role
- A role is a named of list o permissions defined by IAM
- Child policies can not restrict access granted at the parent level

## IAM Conditions

- Allows us to enforce conditional, attribute based control for Google Cloud resources
- We can grant resources access to identities (members) only if configured conditions are met
- IAM conditions are specified in the role bindings of a resource's IAM policy

## Organization Policies

- It is a configuration of restrictions
- It is defined by configuring a constraint with desired restrictions for the organization
- It is applied to the organization node, folders or projects

## Google Cloud Single Sign-On (SSO)

- We can use Cloud Identity to configure SAML and SSO
- If SAML2 isn't supported, we can use a third-party solution such as ADFS, Ping or Okta

## Service Accounts

- Service Accounts provide an identity for carrying out server-to-server interactions
- Programs running within Compute Engine instances can automatically acquire access tokens with credentials
- Tokens are used to access any service API in our project and any other services that grant access to the service account
- Service accounts are convenient when we are not accessing user data
- Service accounts are identified by an email address
- There are 3 types of service accounts:
    - User created (custom)
    - Built-in:
        - Compute Engine and App Engine default service accounts
    - Google APIs service accounts:
        - Runs internal Google processes on our behalf
- Default Compute Engine service account:
    - It is automatically created per project with auto-generated name and email address
    - It is automatically added as a project Editor
    - By default, it is enabled on all instances created using gcloud Cloud Console
- There are 2 types of Google Service accounts:
    - Google-managed service accounts:
        - All service accounts have Google-managed keys
        - Google stores both the public and private portion of the key
        - Each public key can be used for signing for a maximum of 2 weeks
        - Private keys are never directly accessible
    - User-managed service accounts:
        - Google only stores the public portion of a user-managed key
        - Users are responsible for private key security
        - We can create up to 10 user-managed service account keys per service
        - Can be administered via the IAM API, gcloud or the Console

## IAM Best Practices

- Leverage and understand the resource hierarchy
- Use projects to group resources that share the same trust boundary
- Check the policy granted on each resource and make sure we understand hierarchy
- Use the **principle of least privilege** when granting roles
- Audit policies in Cloud Audit Logs
- Audit membership of groups used in policies
- Grant roles to Google groups instead of individuals
- Service accounts best practices:
    - We need to be careful when granting `serviceAccountUser` role
    - When we create a service account, we should give it a display name that clearly identifies its purpose
    - We should establish key rotation policies and methods
    - We can audit service accounts with `serviceAccount.key.lists()` method
- Use Identity-Aware Proxy (IAP)

## Cloud Audit Logs

- Google Cloud services write audit logs that record administrative activities and accesses within your Google Cloud resources
- Cloud Audit Logs maintain three audit logs: Admin Activity logs, Data Access logs, and System Event logs
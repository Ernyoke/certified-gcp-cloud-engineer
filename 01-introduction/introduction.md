# Introduction

## The Google Cloud Platform Resource Hierarchy

- All the resources we use in GCP are organized into projects
- Projects can be organized into folders
- Folders can be brought together into organization nodes
- Projects, folder and organization nodes are all the places where policies can be defined
- Policies are inherited downwards in the hierarchy
- Projects can have different owners and users. They are built separately and they are managed separately
- Each project has a name and a unique project ID
- Optionally projects can be added to folder. In oder to use folders we need an organization node at the top of the hierarchy
- Less restrictive policies at a parent level override a more restrictive policy at the resource level

## Identity and Access Management (IAM)

- Specifies who can take action on specific resources
- Has a who part, can do what part and on which resource part
- There are 3 types of roles:
    - Primitive: they are broad, they are applied to projects. Example: owner, editor, viewer and billing administrator
    - Predefined roles
    - Custom roles: defined by users.
        - They have to be managed
        - They can be used at project or organization level (no folder level)
- Service Accounts: 
    - Provide identities for carrying out server-to-server interactions
    - They are identified with an email address
    - They need to be managed

## Cloud MarketPlace (Cloud Launcher)

- Used to launch predefined services with provided configuration
- The deployed system has to be maintained by the user
# Azure

from: [Microsoft Learn](https://learn.microsoft.com/en-us/collections/n6ga8m0jkgrwk)

## Basic organisations

- Accounts can hold multiple subscriptions
- Subscriptions can hold multiple resources

### Physical infrastucture

- the basic unit are datacenters (with server racks & cooling etc)
- Regions are geographical areas with one or more datacenters

#### Availability Zones

- Availability zones are physically isolated data centers in a region, connected with fibre optic.
- Each zone acts as an isolation boundary, with independent power, cooling & networking.
- services can be
    1. Zonal services, we pinpoint to a specific zone (vm, ip addresses, managed disks)
    2. Zone redundant, automatically replicated across zones (SQL Databases)
    3. Non regional, Redundant to both zonal & regional outages (DNS, Entra ID, Traffic Manager)

#### Region Pairs

- Azure regions are paired with another region within same geography
- To protect against region wise disasters.
- This needs to be configured from the customer
- Data continues to be in same geography for compliance purposes

#### Sovereign Regions

- Isolated from the main instances of Azure
- Examples, US Gov instances and China East, North

### Resource Groups

- Anything that is created, provision or deployed is resource
- Resource groups are groupings of resources
- Each resource must belong to exactly one group.
- Groups cannot be nested or renamed
- Actions to groups cascade, deleting, granting permissions etc
- Example: Dev resources can be a group and be deleted at once.

### Subscriptions

- for organising resource groups and control billing separetly from access
- Subscriptions works are 2 boundries
    1. Biling boundary, seprate biling reports
    2. Access control boundary, spending limits and access rules.

### Managment groups

- Managment groups sit above subscriptions
- Subscriptions can be organised into groups and apply governance policies
- All subscriptions in groups inherit these conditions.
- Unlike resource groups, managment groups can be nested upto 6 level.
- Each Microsft Entra (IAM) tenant has a single tenant root group. 

```
Tenant Root Group
Managment Group (IT, Maketting)
Subscriptions (Apps, Servers)
Resource Groups
Resource (DB, VM)
```


### Virtual Machines

- Basic vms as in any cloud provider
- Name of the VM can be used to determine, type, size, SSD etc
- Virtual machines can be scale sets that are identical load balanced VMs.
- VMs can be in a availbility, meaning reduced change of one event effecting all VMs.
- Availbility can be
    1. Update domain, rebooted at once in planned maintainance
    2. Fault domain, potential power failure at once.

### Virtual Desktops

- Lets users access windows desktops & apps remotely.

### Azure Containers Instances

- Running containers without managing VM's os.

### Azure Container Apps

- These remove the overhead of container managment
- They are a PaaS offering

### Azure Kubernetes Service

- Manages the lifecycle of the containers

```
ACI -> Container Apps -> AKS
```

### Azure Functions

- Event driven, serverless compute
- An event wakes the function, so no need for keeping the resource provisioned
- These can be both stateless or statefull (called Durable Functions)

### Azure AI services

- Azure provides following AI services
    1. AI services, provide acccess to features through APIs
    2. OpenAI services, same but generative etc
    3. AI patterns, built by combining ai services and application logic
    4. Machine Learning, for building, testing & training models.

### IoT & Edge services

- Azure provides following services
    1. IoT Hub, bi directional communication between cloud & IoT
    2. IoT Central, simplified SaaS
    3. IoT Edge, for edge computing


### Application Hosting

- App services can be used to build apps without managing infrastructure

```
VMs -> Containers -> App Service
```

## Networking in Azure

- Virtual networks help connect resources together
- Networks can have private IP ranges that are not internet routable
- We can configure subnets & allocate IP ranges to each
- For name resolution, Azure DNS is used
- Incoming internet connections can be used by public load balancers or public IP address
- On premises resources can be connected by
    1. Point to site, client computer initiates a encrypted VPN connection
    2. Site to site, on premises gateway links to Azure's VPN gateway
    3. ExpressRoute, dedicated private connectivity not over internet

NOTE: when a device wants to connect outside the network it sends the packet to a gateway.

### Filter Networks

- Azure lets you filter traffic between subnets by
    1. Network security groups, have inbound and outbound security rules
    2. Network virtual appliances, specilized hardened VMs for running firewalls, WANs etc

```
Inbound packet -> Security group -> Virtual appliance -> Target VM
```

- Virtual networks can be connected using virtual network peering.
- This traffic between virtual networks is private

### Virtual Private Network

- VPNs are deployed to connect 2 or more trusted networks over untrusted network (internet)
- Traffic is encrypted when travelling over untrusted networks
- connectivity models are
    1. point to site, remote device to azure vnet
    2. site to site, on premises to azure vnet
    3. network to network, between azure vnets
- Types of VPN gateways
    1. Policy based, statically IPs are specified with tunnels to use.
    2. Route based, IP routing (static/dynamic) decides which tunnel to use

- Only one VPN gateway in each network

### High availibility senarios

1. Active/Standby
    - default configuration for VPN gateways
    - Gateways are deployed as 2 instances, even if one resource is shown
    - standby gateway takes over automatically during disruption
2. Active/Active
    - both instances handle trafic simultaneously
    - both have seprate BGP tunnels & IPs
3. ExpressRoute failover
    - VPN gateway can act as an failover for expressroute connections
4. Zone redundant
    - VPN gateways can be deployed in different availability zones

### DNS

- Alias records, when DNS updates when IP of azure resources changes.

## Azure Storage

- Azure provides gloabally unqiue namespace for storage data.
- Types of storage services
    1. Blobs
    2. Files
    3. Queues
    4. Tables

### Storage redundancy

- The type of account determines the storage services and redundancy services
- Redundancy types
    1. Locally Redundant storage
        - atlest 11 nines of durability
        - replicate data three times in primary region
        - all replicas are in same datacenter
        - lowest cost
    2. Zone Redundant storage
        - atlest 12 nines of durability
        - replicate data three times across 3 availbility zones in primary region
    3. Geo redundant storage
        - LRS across both regions
        - atlest 16 nines of durability
    4. Geo zone redundant storage
        - ZRS in primary region and LRS in secondary region
        - 3 availbility zones in primary and 1 LRS in secondary
        - atlest 16 nines of durability

__NOTE__: For redundancy in secondary region, the interval between most recent writes
in primary region and last writes in secondary region is called `recovery point objective`.
RPO dictates the time to which data can be restored. Its typically around 15mins.

### Storage services

- Core data services
    1. Azure blobs, object store for text and binary data (also big data)
        - Can be of tiers, Hot > cool > cold > archive
    2. Azure files, managed file shares
    3. Azure queues, messaging store for reliable messaging between applications components
    4. Azure disks, Block-level storage for VMs.
    5. Azure tables, NoSQL table for structured, non relational data

### Data migraition options

1. Azure migrate 
    - helps you migrate from on premises to the cloud
    - range of tools for assessment and migrations
    - integrates with Independent software vendors
2. Azure Data Box
    - physical migration service
    - 80 tb storage device is transported.

### Azure file movements

1. AzCopy
    - copy, upload, download blobs and files
2. Azure Storage Explorer
    - GUI to manage files and blobs
    - Uses AzCopy on the backend
2. Azure File Sync
    - Bi directional sync with azure
    - frequent files can be replicated locally, others are kept in the cloud

## Identity and Access Managment

- Microsoft Entra ID cloud based identity and access managment
- This are called Directory services
- Features
    1. Authentication
    2. Single sign on
    3. Application managment
    4. Device managment

- On premises Active directory can be connected with Microsoft Entra ID using Entra connect bridges

### Domain services

- Domain is a collection of users, computers and resources, managed centrally
- When domain `joins` a users, meaning user is added to domain

### Group Policy

- Allows admins to configure user and computer settings centrally
- When users signin these policies apply automatically.
- Like for example,

```
Finance User
    Require MFA
    Lock screen after 5min
    Install finance app
```

### LDAP

- Lightweight directory access protocol.
- Language used to talk with directory, can query and update

### External Identities

- For iniviting external partners, vendors etc to access resources
- no need for creating seprate identities for external users
- Our team still enforces access policies

### Conditional Access

- Allow access to resources based on identity signals
- where user is, what device, who the user is

### Role based access control

- Role based access control is applied to scopes
- Scopes are managment groups, subsscriptions, resource groups

### Zero Trust Model

- Verify explicitly, always authenticate and authorize based on all data points
- Least privilage, limit users to Just In Time and Just Enough Access
- Assume breach, limit potential impact and segment access

### Defence in depth

- Uses series of mechanisms to slow advance of an attack
- It has layers provides protection so if one is breached, subsequent layer is in place.
- It includes,
    1. Identity and access, access is granted to only what's needed & signin events and changes are logged
    2. Perimeter, against network based attacks ex, DDoS attacks.
    3. Network, limiting network connectivity to prevent spreading of attacks
    4. Compute, making sure computing resources are secure
    5. Application, Integration into application development lifecycle.
    6. Data, Store and control access to data.

### Key managment

- Means encryption at rest and in transit
- It also includes, Key Vault
    1. Secrets
    2. Encryption keys
    3. Certificates
- Key Vault is useful in 3 ways
    1. Access control
    2. Key rotation
    3. Usage Auditing, Tracking usage

## Identity & Access Managment

- IAM system provides,
    1. Identity managment: creating, storing & managing identity info.
    2. Identity federation: Allows users with account elsewhere to access your system. 
    3. Authenctication: confirm user's identity claim
    4. Authorization: Defining what permissions a user has
    5. Access Control: Enforcing authorization rules
    6. Reporting & Monitoring

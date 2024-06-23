# Cloud Computing

from: [learn.microsoft.com](https://learn.microsoft.com/en-us/training/modules/describe-cloud-compute)

computing on someone else's computer

### Cloud Services

1. Infrastructure as a Service (IaaS)

- hardware, connectivity, physical security is managed
- for Lift-and-Shift migration or Testing and Development

2. Platform as a Service (PaaS)

- hardware, connectivity, physical security
- os, complete development enviroment is managed
- includes licensing and patching os and dbs
- scalability, high uptime and multi-tenet capability included
- for analytics and business intelligence

3. Software as a Service (SaaS)

- renting a fully developed application
- financial software, messaging apps


### Shared Responsibility Model

shared responsibility between customer and cloud provider
customer resposibility depending on cloud service type
on premises > IaaS > PaaS > SaaS

- When using a cloud provider, you’ll always be responsible for:

1. The information and data stored in the cloud
1. Devices that are allowed to connect to your cloud
1. The accounts and identities 

- The cloud provider is always responsible for:

1. The physical datacenter
1. The physical network
1. The physical hosts

- Your service model will determine responsibility for things like:

1. Operating systems
1. Network controls
1. Applications
1. Identity and infrastructure

### Cloud Models

3 main models depending on public availablity

- Private Cloud (for single entity maybe managed by third party)
- Public Cloud (for Anyone you wants to purchase resources)
- Hybrid Cloud (you choose which part is in public and which is private)
- Multi Cloud (you use more than one cloud providers)

`Azure Arc` help to manage your cloud in any model

### Consumption Based Model

Capital Expenditure (CapEx) is one time, up front
Operational Expenditure (OpEx) is over time

Cloud Computing is OpEx as you pay for IT resources you use, meaning 

- no upfront costs
- pay for resources only when they are needed
- no need to mantain infrastructure that is not used to its potential

### Terms Associated

1. Uptime

other term for avaliability
Every cloud service has a SLA (Service Level Agreement)
SLA determines the uptime of service, and determine credits incase of violations

2. Scalability

Ability to adjust resources to meet demand

- Vertical, increase capability of resources
- Horizontal, increase no of resources

3. Reliability

Ability to recover from failure
Clouds being decentralized are resilient

4. Predicatability

- preformance (autoscaling, load balancing, high avaliability)
- cost (resourse monitoring, data analytics)



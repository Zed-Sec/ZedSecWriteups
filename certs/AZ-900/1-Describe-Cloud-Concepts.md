# Describe cloud computing

## Define cloud computing

### What is cloud computing?
	
Cloud computing is the delivery of computing services over the internet. Computing services include common infrastructure such as VMs, storage, databases and networking. Cloud services can also include things like Internet of Things (IoT) and machine learning. The main benefit of cloud computing is the ability to rapidly scale.

## Describe the shared responsibility model

Responsibilities such as maintaining infrastructure and patching systems are shared between the customer and the cloud provider. Physical security, power, cooling, and network connectivity are the responsibility of the cloud provider.

The customer is responsible for the data and information stored in the cloud. The customer is also responsible for security.

Depending on which service you're using the responsibility changes. With a cloud SQL database, the could provider would be responsible for maintaining the actual database but you're responsible for the data that's ingested into the database.

The below figure highlights how the Shared Responsiblity Model informs who is responsible for what, depending on the service type.

![SharedResponsibilityModel](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-compute/media/shared-responsibility-b3829bfe.svg)

The customer is always responsible for:

* The information and data stored in the cloud.
* Devices that are allowed to connect to your cloud.
* The accounts and identities of the people, services and devices within your organization.

The cloud provier is always responsible for:

* The physical datacenter.
* The physical network.
* The physical hosts.

The service model being used determines the responsibility for:

* Operating systems.
* Network controls.
* Applications.
* Identity and infrastructure.

## Define cloud models, including public, private, and hybrid

### Private cloud

The private cloud is cloud services delivered over the internet to a single entity, much like a physical datacenter for an IT department.

### Public cloud 

Built by a third-party cloud provider. The services of a public cloud are available to anybody that buys the services.

### Hybrid cloud

A hybrid cloud uses both private and public together in an inter-connected environment. Hybrid cloud can be used to offer an extra layer of security.

### Multi-cloud

Multi-cloud deals with two or more public cloud providers and manage resources and security in both environemnts.

### Azure Arc

Allows you to manage your cloud environment.

### Azure VMware Solution

Allows you to migrate VMware private cloud environments to a public or hybrid cloud.

## Identify appropriate use cases for each cloud model

The key differences between cloud types:

| Public cloud | Private cloud | Hybrid cloud |
| - | - | - |
| No capital expenditures to scale up. | Organizations have complete control over resources and security. | Provides the most flexibility.
| Applications can be quickly provisioned and deprovisioned | Data is not collocated with other organizations' data | Organizations determine where to run their applications. |
| Organization pay only for what they use. | Hardware must be purchased for startup and maintenance. | Organizations control security, compliance, or legal requirements. |
| Organizations don't have complete control over resources and security. | Organizations are responsible for hardware maintenance and updates. | |

## Describe the consumption-based model

The two main types of expense are capital expenditure (CapEx) and operational expenditure (OpEx).

CapEx is typicall one time, up-front payment to secure a tangible resource. A new building, repaving the parking lot, building a datacentre, or buying a company vehicle.

OpEx is the cost of a service over time, such as leasing a company vehicle, or signin gup for cloud services.

Cloud computing follows a consumption-based model, which means that you pay for the resources you use. The benefits of this are:

* No upfront costs.
* No need to purcahse and manage costly infrastructure that users might not use to its fullst potential.
* The ability to pay for more resources when needed.
* The ability to stop paying for the resources that aren't needed anymore.

With a traditional infrastructure it's difficult to estimate the exact costs needed, it's easy to not budget enough and have to spend more expenditure or to budget too much and have unused resources. Resources can be scaled up and down easily.

## Compare cloud pricing models

The pay-as-you-go pricing model of the cloud allows you to:

* Plan and manage operating costs.
* Run infrastructure modre efficiently.
* Scale as your business needs change.

You're billed for only what you end up using.

# Describe the benefit of using cloud services

## Describe the benefits of high availability and scalability in the cloud

### High availability

High availibility is the focus on making sure resources are available, regardless of which disruptions are caused.

### Scalability

Scalability allows resources to be adjusted on demand. In times or great demand, resources can be scaled up temporarily and scaled back down to save costs when traffic is lower.

* Vertical scaling
  * When developing an application, if you need more processing power, you can vertically scale up to add more CPUs or RAM to the virtual machine. If you have too many resources you can vertically scale down.
* Horizontal scaling
  * With horizontal scaling, if you suddently experience a jump in demand, you can scale out horizontally by adding extra VMs.

## Describe the benefits of reliability and predictability in the cloud

### Reliability

Reliability is the ability of a sytem to recover after failure and continue to function. The cloud naturally supports this by design. Using a cloud service, resources can be deployed in regions around the world. This allows other regions to remain functional if one region goes down.

### Predictability

Predictability allows you to focus on cost or performance predictability.

* Performance
  * Focuses on predicting the resources needed to provide a positive experience for your customers. Autoscaling, load balancing, and high availability are some of the concepts that support performance predictability.
* Cost
  * Forecasting the cost of the cloud spend. Costs can be tracked in real time, data analytics can also be applied to make sure you're running in the most efficient way. There are tools such as the Toital Cost of Ownership and the Pricing Calculator that will give an estimate of potential cloud spends.

## Describe the benefits of security and governance in the cloud

Cloud features support governance and compliance. Set templates can be used to make sure that resources are meeting your defined corporate standards. If you need to update the standards, all deployed resources can be changes with ease.

## Describe the benefits of manageability in the cloud

There are two types of manageability for the cloud:

* Management of the cloud - speaks to managing your cloud resources
  * Automatically scale resource deployment based on needs.
  * Deploy resources based on a preconfigured template, removing the need for manual configuration.
  * Monitor the health of resources and automatically replace failing resources.
  * Recieve automatic alerts based on configured metrics, so you're aware of performance in real time.
* Management in the cloud - Speaks to how you're able to manage your cloud environment and resources   
  * Web portal.
  * Command line interface.
  * API.
  * PowerShell.

# Describe cloud service types

## Describe infrastructure as a service (IaaS)

The cloud provider is responsible for the hardware, network connectivity, and physical security. You're responsible for everything else: operating system isntallation, configuration, and maintenance.

## Describe platform as a service (PaaS)

Middle ground between renting space in a datacentre and paying for a complete and deployed solution. The cloud provider maintains everything they maintain for IaaS, but also the operating systems, business tools. It is well suited to provide a complete development environment without the maintenance.

## Describe software as a service (SaaS)

SaaS is the most complete cloud service from a product perspective. With SaaS, you're essentially renting or using fully developed application. Email, financial software, messaging applications are all ciommon examples of SaaS implementation.

## Identify appropriate use cases for each cloud service (IaaS, PaaS, SaaS)

* IaaS
  * Lift-and-shift migration - standing up cloud resources similar to your on-prem datacentre, and then simply moving the things running on-prem to your IaaS infrastructure.
  * Testing and development - You have established configurations for development and test environments that you need to rapidly replicate. You can stand up or shut down the different environments rapidly with an IaaS structure, while maintaining complete control.
* PaaS
  * Development framework is provided and allows developers to use built-in software components in the PaaS, reducing coding work.
  * Analytics or business intelligence - Tools provided as a service with PaaS allow organization to analyze and mine their data, finding insights and platforms and improving forecasting.
* SaaS
  * Email and messaging.
  * Business productivity applications.
  * Finance and expense tracking.
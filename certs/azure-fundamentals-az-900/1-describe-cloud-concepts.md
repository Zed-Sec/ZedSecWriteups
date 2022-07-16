# 1 - Describe Cloud Concepts

## 1.1 - Introduction to Azure Fundamentals

### What is cloud computing?

Cloud computing is the delivery of computing services over the internet, using a pay-as-you-go pricing model. You only pay for the resources that you use which can help:

* Lower operating costs.
* Run infrastructure more efficiently.
* Scale as the needs of the business change.

You can scale cloud computing up when demand is high and once it lowers then you can give some of the resources back. Another benefit of this is that you don't have to maintain your own physical datacentre.

### What is Azure?

Azure is a collection of cloud services from Microsoft.

### Azure Services

Azure has many available services find an infographic with some of these services below:

![](<../../.gitbook/assets/image (1).png>)

Some of the more commonly used categories are:

* Compute
* Networking
* Storage
* Mobile
* Databases
* Web
* Internet of Thins (IoT)
* Big data
* AI&#x20;
* DevOps

#### Compute&#x20;

Compute services are often one of the primary reasons why companies move to the Azure platform, an example of some of these services offered for compute are below:

| Service name                     | Service function                                                         |
| -------------------------------- | ------------------------------------------------------------------------ |
| Azure Virtual Machines           | Windows or Linux VMs hosted in Azure.                                    |
| Azure Virtual Machine Scale Sets | Scaling for Windows or Linux VMs hosted in Azure.                        |
| Azure Kubernetes Service         | Cluster management for VMs that run containerized services.              |
| Azure Service Fabric             | Distributed systems platform that runs in Azure or on-premises.          |
| Azure Batch                      | Managed service for parallel and high-performance computing application. |
| Azure Container Instances        | Containerized apps run on Azure without provisioning servers or VMs.     |
| Azure Functions                  | An event-driven, serverless compute service.                             |

#### Networking

Linking compute resources and providing access to applications is the key function of Azure networking. Some examples:

| Service name                   | Service function                                                                     |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| Azure Virtual Network          | Connects VMs to incoming VPN connections.                                            |
| Azure Load Balancer            | Balances inbound and outbound connections to applications or service endpoints.      |
| Azure Application Gateway      | Optimizes app server farm delivery while increasing application security.            |
| Azure VPN Gateway              | Accesses Azure Virtual Networks through high-performance VPN gateways.               |
| Azure DNS                      | DNS services.                                                                        |
| Azure Content Delivery Network | Delivers high-bandwidth content to customers globally.                               |
| Azure DDoS Protection          | Protects Azure-hosted application from distributed denial of service (DDOS) attacks. |
| Azure Traffic Manager          | Distributes network traffic across Azure regions worldwide.                          |
| Azure ExpressRoute             | Connects to Azure over high-bandwidth dedicated secure connections.                  |
| Azure Network Watcher          | Monitors and diagnoses network issues using scenario-based analysis.                 |
| Azure Firewall                 | Implements high-security, high-availability firewall with unlimited scalability.     |
| Azure Virtual WAN              | Created a wide area network (WAN) that connects to local and remote sites.           |

#### Storage

Azure provides four main types of storage services:

| Service name        | Service function                                                                                                                               |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Azure Blob Storage  | Storage service for very large objects, such as video files or bitmaps.                                                                        |
| Azure File Storage  | File shares that can be accessed and manager like a file server.                                                                               |
| Azure Queue Storage | A data store for queuing and reliably delivering messages between applications.                                                                |
| Azure Table Storage | Table storage is a service that stores non-relational structured data in the cloud, providing a key/attribute store with a schema less design. |

These services share several common attributes:

* **Durable** - highly available with redundancy and replication.
* **Secure -** through automatic encryption and role-based access control (RBAC).
* **Scalable -** with virtually unlimited storage.
* **Managed -** handling maintenance and any critical problems for you.
* **Accessible -** using HTTP or HTTPS.

#### Mobile

Azure devs can create mobile back-end services for iOS, Android, and Windows apps. Features that used to take time and increase project risk are now simple to include. Other features of this service include:

* Offline data sync.
* Connectivity to on-premises data.
* Broadcasting push notifications.
* Autoscaling to match business needs.

**Databases**

Azure provides multiple DB services to store a wide variety of data types and volumes:

| Service name                         | Service function                                                                                     |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Azure Cosmos DB                      | Globally distributed database that supports NoSQL options.                                           |
| Azure SQL Database                   | Fully managed relational database with auto-scale, integral intelligence, and robust security.       |
| Azure Database for MySQL             | Fully managed and scalable MySQL relational database with high availability and security.            |
| Azure Database for PostgreSQL        | Fully managed and scalable PostgreSQL relational database with high availability and security.       |
| SQL Server on Azure Virtual Machines | Service that hosts enterprise SQL Server apps in the cloud.                                          |
| Azure Synapse Analytics              | Fully managed data warehouse with integral security at every level of scale.                         |
| Azure Database Migration Service     | Service that migrates databases to the cloud with no application code change.                        |
| Azure Cache for Redis                | Fully managed service caches frequently used and static data to reduce data and application latency. |
| Azure Database for MariaDB           | Fully managed and scalable MariaDB relational database with high availability and security.          |

#### Web

Azure includes several services to build and host web apps and HTTP-based web services:

| Service name                          | Service function                                           |
| ------------------------------------- | ---------------------------------------------------------- |
| Azure App Service                     | Quickly create powerful cloud web-based apps.              |
| Azure Notification Hub                | Send push notifications to any platform from any back end. |
| Azure API Management                  | Public APIs at scale.                                      |
| Azure Cognitive Search                | Deploy this fully manages search as a service.             |
| Web Apps feature of Azure App Service | Create and deploy mission-critical web apps at scale.      |
| Azure SignalR Service                 | Add real-time web functionalities easily.                  |

#### IoT

Many services can assist IoT devices on Azure:

| Service name  | Service function                                                                                                                                                                                    |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IoT Central   | Fully managed global IoT software as a service (SaaS) solution that makes it easy to connect, monitor, and manage IoT assets at scale.                                                              |
| Azure IoT Hub | Messaging hub that provides secure communications between and monitoring millions of IoT devices.                                                                                                   |
| IoT Edge      | Fully managed service that allows data analysis model to be pushed directly onto IoT devices, which allows them to react quickly to state changes without needing to consult cloud-based AI models. |

#### AI

Some of the most common AI and machine learning service types in Azure:

| Service name                   | Service function                                                                                                                                                         |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Azure Machine Learning Service | Cloud-based environment you can use to develop, train, test, deploy, manage and track machine learning models.                                                           |
| Azure ML Studio                | Collaborative visual workspace where you can build, test, and deploy machine learning solutions by using prebuilt machine learning algorithms and data-handling modules. |
|                                |                                                                                                                                                                          |

#### DevOps

DevOps brings together processes and technology by automating software delivery to provide continuous value to your users. With ADO, you can create **build** and **release** pipelines that provide continuous integration, delivery and deployment for applications. You can integrate repositories and application tests, perform application monitoring, and work with build artifacts. You can also work with backlog items for tracking, automate infrastructure deployment, and integrate a range of third-party tools and services such as Jenkins and Chef.

### Azure Accounts

To create and use Azure services, you need an Azure subscription. When you create an Azure account a subscription is created for you. Once you've created the account you can create additional subscriptions, such as a subscription for development, marketing, sales, etc. Once you've created a subscription you can start creating resources within each subscription.

![](<../../.gitbook/assets/image (1) (1).png>)

You can create a free account which gives access to:

* Free access to Azure products for 12 months.
* A credit to spend for the first 30 days.
* Access to more than 25 products that are always free.

Students can also create an account which gives $100 free credit and free developer tools to play around with.

## 1.2 Discuss Azure fundamental concepts

### Public, Private, and Hybrid clouds

There are three deployment models for cloud computing:

| Deployment model | Description                                                                                                                                                                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Public cloud     | Services are offered over the public internet and available to anybody who wants to purchase them. Cloud resources, such as servers and storage, are owned and operated by a third-party cloud service provider, and delivered over the internet.     |
| Private cloud    | A private cloud consists of computing resources used exclusively by users from one business or organization. A private cloud can be physically located at your organization's on-site datacenter, or can be hosted by a third party service provider. |
| Hybrid cloud     | A mix between the two, allowing data and applications to be shared between public and private resources.                                                                                                                                              |

### Cloud Model Comparison

**Public Cloud:**

* No capital expenditure to scale up.
* Applications can be quickly provisioned and deprovisioned.
* Organizations pay only for what they use.

**Private Cloud:**

* Hardware must be purchased for start-up and maintenance.
* Organizations have complete control over resources and security.
* Organizations are responsible for hardware maintenance and updates.

**Hybrid Cloud:**

* Provides the most flexibility.
* Organizations determine where to run their applications.
* Organizations control security, compliance, or legal requirements.

### Benefits and considerations of cloud computing

**Advantages**&#x20;

* **High availability -** Depending on the SLA, your cloud-based apps can provides continuous user experience with no apparent downtime.
* **Scalability -** Apps in the cloud can scale vertically and horizontally:
  * Vertically to increase compute capacity adding RAM or CPU to a virtual machine.
  * Horizontally by adding resources such as more VMs to the configuration.
* **Elasticity -** You can configure cloud-based apps to take advantage of auto-scaling, so your apps always have the resources they need.
* **Agility -** Deploy and configure cloud-based resources quickly as your app requirements change.
* **Geo-distribution -** You can deploy apps and data to different datacenters around the globe. This allows consistent customer experience all over the world.
* **Disaster recovery -** By taking advantage of cloud-based backup services, data replication, and geo-distribution, you can deploy your apps with the confidence that comes from knowing your data is safe in the event of disaster.

**Capital expenses vs. operating expenses**

There are two different types of expenses that you should consider:

* **Capital Expenditure (CapEx) -** is the up-front spending of money on physical infrastructure, and then deducting that up-front expense over time. The up-front cost from CapEx has a value that reduces over time.
* **Operational Expenditure -** is spending money on services of products now and being billed for them now. You can deduct this expense the same year you spend it. There is no up-front cost as you pay for services as you use them.

**Consumption-based model**

Cloud computing is a consumption-based model, meaning users only pay for the resources that they use. The benefits of this are:

* No upfront costs.
* No need to purchase or manage infrastructure.
* The ability to pay for additional resources as they are needed.
* The ability to stop paying for resources that are no longer needed.

### Different cloud service models

| Model | Definition                  | Description                                                                                                                                                                                                                                                                                                                    |
| ----- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| IaaS  | Infrastructure-as-a-Service | Cloud provider keeps the hardware up-to-date, but operating system maintenance and network config is up to the user. This model allows you to set up and manager your own virtual machines.                                                                                                                                    |
| PaaS  | Platform-as-a-Service       | The cloud provider manages the virtual machines and networking resources, and the cloud tenant deploys their applications into the managed hosting environment. Azure App Services provides a managed hosting environment where developers can upload web applications without having to manage the underlying infrastructure. |
| SaaS  | Software-as-a-Service       | The cloud provider manages all aspects of the application environment. The cloud tenant only needs to provide their data to the application. For example, Office 365.                                                                                                                                                          |

**IaaS**

* **Advantages**&#x20;
  * No CapEx - Users have no up-front costs.
  * Agility - applications can be made accessible quickly, and deprovisioned whenever needed.
  * Management - The users maintain the services they provision and the provider maintains the cloud infrastructure.
  * Consumption-based model - Organizations pay only for what they use.
  * Skills - Deep technical skills aren't required to use, and gain the benefits of a public cloud.
  * Cloud benefits - Organizations can use the skills and expertise of the cloud provider to ensure workloads are made secure and highly available.
  * Flexibility - IaaS is the most flexible cloud service because you have control to configure and manage the hardware running your application.

**PaaS**

* **Advantages**
  * No CapEx.
  * Agility.
  * Consumption-based model.
  * Skills.
  * Cloud benefits.
  * Productivity - Users can focus on application development only.
* **Disadvantages**
  * Platform limitations - There may be some limitations to the platform.

**SaaS**

* **Advantages**
  * No CapEx.
  * Agility.
  * Pay-as-you-go pricing model - Users pay for the software that they use.
  * Skills.
  * Flexibility.
* **Disadvantages**
  * Software limitations - You don't have control over software features.

**Cloud service model comparison**

![](../../.gitbook/assets/image.png)

### **Serverless Computing**

Like PaaS, serverless computing enables developers to build applications faster by eliminating the need for them to manage the infrastructure. With a serverless application, the cloud service provider automatically provisions, scales and manages the infrastructure required to run the code.

This is only considered serverless because the developer doesn't need to manage the server.

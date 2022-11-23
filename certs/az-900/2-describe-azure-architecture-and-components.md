# 2 - Describe Azure Architecture and Components

## Describe the core architectural components of Azure

![AzureDiagram](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-core-architectural-components-of-azure/media/account-scope-levels-9ceb3abd.png)

### Describe Azure regional, regional pairs, and sovereign regions

#### Regions

A geographical area on the planet that contains at least one, but could be multiple, Azure Datacentres.

#### Region pairs

Most regions in Azure are paired with another region within the same geography (such as US, Europe, or Asia). This allows repliation of resources across a geography that helps reduce the chances of an outtage.

If a region is hit by a natural disaster, the services would fail over to the other region in the pair.

![RegionPairs](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-core-architectural-components-of-azure/media/region-pairs-7c495a33.png)

#### Sovereign Regions

Sovereign regions are Azure instancs that are isolated from the main instance of Azure. You might need one for compliance or legal reasons.

### Describe availability zones

An availability zone is a physically seperate datacentre withing an Azure region. Each is made up of one or more datacentres, each with dedicated power and cooling. It's setup as an isolation boundary so that if one goes down, the other continues to work.

### Describe Azure datacentres

The Azure datacentres are similar to a large corporate datacentre. Large facilities are used to house serveral high powered machines, held in racks, that are setup with dedicated power, cooling, and networking.

### Describe Azure resources and resource groups

#### Resources

A resoure is anything that is created or deployed within Azure.

#### Resource groups

A way to group resources. When you create a resource, you're required to put it into a resource group. A resource can only belong to one resoure group at a time. Resources can be moved between groups, forgoing it's relationship with the original group.

* Can't be nested.
* Actions applied to the resource group apply to all of the members of the group.
* If you delete a resource group, all resources it contains are deleted.
* If you're granted or denied access to a resource group, that applies to all the resources within too.

### Describe subscriptions

Azure subscriptions allows you to organize resource groups and billing.

![Subscriptions](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-core-architectural-components-of-azure/media/subscriptions-d415577b.png)

To use Azure you have to be using a subscription. A subscription allows you to authenticate and be authorized to the resources within. It also allows you to provision resources.

One subscription is required but it's possible to have multiple.

If you have multiple subscriptions you can set up a subscription boundary:

* Billing boundary: This determines how an Azure account is billed. Azure generates separate billing reports for each subscription. Allowing cost management to be organized.
* Access control boundary: Access-management policies are at the subscription-level. This allows you to break down billing to the specific users that provision specific resources within a subscription.

### Describe management groups

Resources are put into resource groups, resource groups are grouped into subscriptions. Multiple subscriptions can be placed into a management group. All subscriptions within the management group inherit the governance from the management group.

### Describe the hierarchy of resource groups, subscriptions, and management groups

![ManagementGroup](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-core-architectural-components-of-azure/media/management-groups-subscriptions-dfd5a108.png)

Management groups can be nested.

Examples of management group use cases:

* Create a hierarchy that applies a policy: You can limit VM locations to the US West Region in a group called Production. The permissions inherit onto the subscriptions within the management group and so will apply to all VMs nested within.
* Provide user access to multiple subscriptions: Moving multiple subscriptions into a management group allows you to create one Azure role-based access control (RBAC) on the management group. This allows people with a specific role to be assinged access to multiple subscriptions and resources with ease.

Characteristics of management groups:

* 10,000 management groups can be supported within a single directory.
* A management group can go up to six levels of depth, not including the root directory.
* Each management group and subscription can only have one directly above it.

## Describe Azure compute and networking services

### Compare compute types, including container instances, virtual machines (VMs), and functions

#### Containers

Containers are similar to VMs except you don't need to manage the operating system. They're designed to be lightweight and scaled out with ease while being more agile than traditional VMs.

#### VMs

VMs can be configured in Azure as infrastructure as a service (IaaS).

#### Azure Functions

Azure Functions are event-drive, serverless compute options that don't require the maintaining of VMs or Containers that have to be kept running. Functions can sit dormant, waiting to activate on a specific event, saving resources.

### Describe VM options, including Azure Virtual Machines, Azure Virtual Machine Scale Sets, availability sets, and Azure Virtual Desktop

#### Virtual machine scale sets

You can run a single VM, or group them together to provive high availability, scalability, and redundancy. A scale set is a group of identical, load-balanced VMs. This allows you to quickly scale up and back down VMs.

#### Virtual machine availability sets

Allows you to stagger updates with varied power and network connectivity options, allowing your VMs to remain available if some go down.

#### Azure Virtual Desktop

Another type of virtual machine. Azure Virtual Desktop is a cloud-hosted version of Windows that can be accessed remotely.

### Describe resources required for virtual machines

When provisioning a VM, you can specify:

* Size (purpose, number of processor cores, and amount of RAM)
* Storage disks (hard disks, solid state drives)

### Describe application hosting options, including the Web Apps feature of Azure App Service, containers and virtual machines

There are a few services on Azure that can be utilised for hosting applications. VMs give the ability to have maximum control over the hosting environment. Containers allow for isolation in a hosting solution.

#### Azure App Service

The third hosting option is the Azure App Service. This allows you to create and host web apps, background jobs, mobile back-ends, REST APIs. You can use the progamming language of your choice without having to manage the underlying operating system.

The most common app service types:

* Web apps
* API apps
* Webjobs
* Mobile apps

### Describe virtual networking, including the purpose of Azure Virtual Networks, Azure virtual subnets, peering, Azure DNS, Azure VPN Gateway, and Azure ExpressRoute

#### Describe Azure Virtual Networking

Azure virtual networks and virtual subnets enable Azure resources to communicate with eachother, users on the internet, and with machines on-prem.

Azure virtual networks provide the following key networking capabilities:

* Isolation and segmentation - Azure allows you to create isolated networks. When you set up a virtual network, you define a private IP address space by using either public or private IP address ranges. The IP range only exists within the virtual network and isn't internet routable. That IP space can be subnetted. Virtual networks can be configured to use either an internal or external DNS server.
* Internet communications - Incoming connections fromt he internat can be enabled by assigning an Azure resource with a public IP address, or by putting the resource behind a public-facing load balancer.
* Communiction between Azure resources - You can enable comunication between Azure resources in the following ways:
  * Virtual networks can connect VMs and also other Azure resources, such as, App Service for Power Apps, Azure Kubernetes Service, and Azure virtual machine scale sets.
  * Service endpoints can connect to other Azure resource types, such as, Azure SQL databases and storage accounts. This allows you to link multiple Azure resources to virtual networks to improve security and provide optimal routing between resources.
* Communication between on-prem resources
  * Point-to-site virtual private network connections - from a computer outside your org, back to your corporate network. The client initiates an encrypted VPN connectiont o connect to the Azure virtual network.
  * Site-to-site - links on-prem VPN device or gateway to the Azure VPN gateway in a virtual network. Makes Azure devices appear as being on the local network. The connection is encrypted and works over the internet.
  * Azure ExpressRoute - Dedicated private connectivity to Azure that doesn't travel over internet. Used when you need large bandwidth and security.
* Route network traffic - Azure routes traffic between subnets on any connected virtual networks, on-premises networks, and the internet. You can control those settings though:
  * Route tables allow you to define how traffic should be directed.
  * Border Gateway Protocol (BGP) works with Azure VPN gateways, Azure Route Server, or Azure ExpressRoute to propagate on-premisies BGP routes to Azure virtual networks.
* Filter network traffic - Traffic between subnets can be filtered via:
  * Network security groups - Azure resources that can contain inbound and outbound security rules that allow or block traffic, based on the information that makes up the traffic such as source and destination IP address, port, and protocol.
  * Network virtual appliances - VMs that carry out a specific function such as a firewall or WAN optimization.
* Connect virtual networks - Virtual networks can be linked via peering. Peering allows two virtual networks to be connected. Traffic between peered networks is private.

#### Azure Virtual Private Networks

An encrypted tunnel within another network, used to connect two or more trusted private networks. VPN gateways are deployed in dedicated subnets of a virtual network.

#### Azure ExpressRoute

Dedicated private connectivity to Azure that doesn't travel over internet. Used when you need large bandwidth and security.

#### Azure DNS

Hosting service for DNS domains, provides name resolution by using Microsoft Azure Infrastructure.

Azure DNS benefits:

* Reliability and performance
* Security
* Ease of Use
* Customizable virtual networks
* Alias records

### Define public and private endpoints

When interacting with an internet-facing resource within Azure you can use a public endpoint. You still need to authenticate to the services you're accessing via a public endpoint.

Private endpoints are accessed via IP addresses within a subnet you specify.

## Describe Azure storage services

### Compare Azure storage services

Azure storage services:

* Azure Blobs - A massively scalable object store for text and biary data. Also includes support for big data analytics through Data Lake Storage Gen2.
* Azure Files - Managed file shares for cloud or on-premises deployments.
* Azure Queues - A messaging store for reliale messaging between application components.
* Azure Disks - Block-level storage volumes for Azure VMs.

### Describe storage tiers

Azure storage offers different access tiers for blob storage:

* Hot access - Data that is accessed frequently.
* Cool access - Data that is infrequently accessed and stored for at least 30 days.
* Archive access tier - Appropriate for the data that is rarely accessed and stored for at least 180 days, with flexible latency requirements.

### Describe redundancy options

Azure storage always stores multiple copies of your data so that it's protected from planned and unplanned events.

#### Redundancy in the primary region.

Data in Azure Storage is always replicated three times in the primary region. There's two options for how this works:

*   Locally redundant storage - LRS replicates your data three tiems within a single data centre in the primary region. this is the lowest cost redundancy option offered but also offers the least durability.

    ![LRS](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-azure-storage-services/media/locally-redundant-storage-37247957.png)
* Zone-redundant storage - ZRS replicates across three availability zones in the primary region. With this option, data is available even if a zone becomes unavailable.

#### Redundancy in the secondary region

When an application requires high durability, you can choose to copy the data in your storage account to a secondary region. When selecting a secondary region, it's based on region pairs and isn't able to be changes.

* Geo-redundant storage - GRS copies three times to a single physical location within the primary region using LRS. The to a single phsyicsl location within the secondary region. ![GRS](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-azure-storage-services/media/geo-redundant-storage-3432d558.png)
* Geo-zone-redundant storage - GZRS combiens the high availability provided by redundancy across availability zones with protection from regional outages provided by geo-replication. Data in a GZRS storage account is copies across three availability zones in the primary region and also is replicated to a secondary geographical region. ![GZRS](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-azure-storage-services/media/geo-zone-redundant-storage-138ab5af.png)

### Describe storage account options and storage types

A storage account allows you to configure data to be accessible anywhere in the world over HTTP or HTTPS. When you create a storage account you pick the storage account type, this specifies the storage services and the redundancy options.

| Type                        | Supported Services                                      | Redundancy Options                   | Usage                                                                     |
| --------------------------- | ------------------------------------------------------- | ------------------------------------ | ------------------------------------------------------------------------- |
| Standard general purpose v2 | Blob storage, Queue Storage, Table Storage, Azure Files | LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS | Standard storage account type for blobs, file shares, queues, and tables. |
| Premium block blobs         | Blob Storage (including Data Lake Storge)               | LRZ, ZRS                             | Premium storage account type for block blobs and append blobs.            |
| Premium file shares         | Azure Files                                             | LRS, ZRS                             | Premium storage account ype for file shares only.                         |
| Premium page blobs          | Page blobs only                                         | LRS                                  | Premium storage account type for page blobs only.                         |

### Identify options for moving files, including AzCopy, Azure Storage Explorer, and Azure File Sync

Azure offers a few services for migration but it also offers some tools for smaller moving jobs.

* AZCopy - CLI utility that you can use to copy blobs or files to or from your storage account.
* Azure Storage Explorer - Standalone app that provides a GUI to manage files and blobs in an Azure Storage account. Wroks on Windows, macOS, and Linux. Uses AZCopy on the backend.
* Azure File Sync - Lets you cenralize files shares in Azure Files while keeping flexibility, performance, and compatibility of a Windows file server.

### Describe migration options, including Azure Migrate and Azure Data Box

* Azure Migrate - Service which helps to migrate from an on-prem environment to the cloud.
* Azure Data Box - Physical migration service that helps transfer large amounts of data quickly. A Data Box storage device is shipped to you and has a maximum capacity of 80 terabytes. Once you've transferred the data to the device, you pack it back up in the rugged case it arrives in and return the Data Box. Once Microsoft receive the data back they'll upload it to the Azure portal.

## Describe Azure identity, access, and security

### Describe directory services in Azure, including Azure Active Directory (Azure AD) and Azure Active Directory Domain services (Azure AD DS)

#### Azure AD

Azure AD is a directory service that enables you to sign in and access both Microsoft cloud applications and cloud applications that you develop. Azure AD can also help you maintain your on-prem AD deployment.

Azure AD is for:

* IT administrators - for controlling access to applications and resources based on their business requirements.
* App developers - Developers can use Azure AD to provide standards-based approach for adding functionaity to applications, such as adding SSO functionality.
* Users - Users can manage their identities and perform self-service password resets.
* Online service subscribers - Most Microsoft products allow users to use their Azure AD credentials to authenticate.

What Azure AD does:

* Authentication - Verifies identity to acces applications and resources. Also provides self-service password reset, MFA, custom list of banned passwords, and smart lockout services.
* Single sign-on - allows users to log into multiple applications with one set of credentials. This is easier for users to remember just on set of passwords but also easier for administrators to disable accounts for multiple services.
* Device management - AD allows you to register devices, this allows these devices to be managed through MDM tools such as Intune and setup Conditional Access which allows access to be restricted to specific accounts regardless of the account that's logging in.

#### Azure AD Domain Services

AS DS provides managed domain services, such as domain join, gorup policy, lightweight directory access protocol (LDAP), and Kerberos/NTLM authentication. With Azure AD DS you can benefit from the directory services without maintaining a bunch of domain controllers.

When you create an Azure AD DS domain, you define a unique namespace, which becomes the domain name. Two Windows Server domain controllers are then deployed into your selected Azure region. This is a replica set. These DCs don't need to be managed, configured or updated. Azure handles all of this.

### Describe authentication methods in Azure, including single sign-on (SSO), multifactor authentication, and passwordless

#### Single sign-on

Allows a user to sign into multiple resources from different providers with the same set of credentials. This makes it easier for user to remember one set of credentials and also for IT admins to revoke account access to multiple solutions at once.

#### Multifactor Authentication

Prompting a user for an extra form (factor) fo itentification during the sign-in process. Multifactor usually asks for two out of three categories:

* Something you know - A question or a password.
* Something you have - A code that expires on a timed basis.
* Something the user is - Like a biometric fingerprint.

#### Passwordless Authentication

Passwordless removes the password and replaces it with soemthing you are, something you have and something you know. An few examples of this:

* Windows Hello - Uses the fingerprint scanner on a laptop or facial recognition to allow authentication.
* Microsoft Authenticator App - When a user signs in a number can be displayed on the screen, the user then has to open up the app and select the matching number.
* FIDO2 security keys - Fast Identity Online promots open authentication standards and reduces the use of password. These keys can be purchased and are typically USBs that are used as a physical security key to login.

### Describe external identities and guest access in Azure

An external identity is a person, device or service, etc, that is outside your oranization. Azure AD External Identities details ways that you can interact with users outside of your organization securely.

With extenal identities, the sexternal person uses their own credentials from their own provider, while the IT admin only has to manage their access.

* Business to business (B2B) collaboration - Allowing an external user to use an identity of their choice to sign into your Microsoft or other enterprise applications. These users are represented as guest users.
* B2B direct connect - A two-way trust with another Azure AD organization to be used for collaboration. Currently this supports shared Teams channels and allowing external users to access resources within their home instance of teams.
* Azure AD business to customer (B2C) - Publish saaS and custom developed apps to consumers and customers while using Azure AD B2C for access management.

![ExternalIdentity](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-azure-identity-access-security/media/azure-active-directory-external-identities-5a892021.png)

### Describe Azure AD Conditional Access

Conditional Access allows AD t allow or deny access to resources based on identity signals. These signals include who the user is, and what device the user is requesting access from, which application the user is trying to access.

### Describe Azure role-based access control (RBAC)

RBAC is the principle of only giving users the access they need for their specific role. Azure RBAC can be applied at the scope level, a scope can be:

* A management group
* Subscription
* Resource Group
* Individual Resources

Azure RBAC is enfored through Azure Resource Manager (ARM).

### Describe the concept of Zero Trust

Zero trust assumes a breach at the outset. The principles of the zero trust model are:

* Verify explicitly - Always authenticate and authorize based on all available data points.
* Use least privilege access - Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.
* Assume breach - Minimize blast radius and segment access. Verify end-to-end encryption. User analytics to get visbility, drive threat detection, and imprve defenses.

### Describe the purpose of the defence in depth model

Defence-in-depth aims to protect information from being accessed and stolen by those who aren't authorized to access it. it aims to slow the advance of an attack that aims to acquire data.

Defence-in-depth uses a layered approach:

![DID](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-azure-identity-access-security/media/defense-depth-486afc12.png)

* Physical Security - First line of defence to protect computing hardware in the datacenter.
* Identity & Access - Controls access to infrastructure and change control.
  * Control access to infrastructure and change control.
  * Use SSO and multifactor authentication.
  * Audit events and changes.
* Perimeter - Uses DDoS protection to filter large-scal sattacks before they can disrupt services for users.
  * Use DDoS proetcion
  * Use perimiter firewalls to identify and alert on malicious attacks on your network.
* Network - Limits communication between resources through segmentation and access controls.
  * Limit communication between resources.
  * Deny by default.
  * Restrict inbound internet access and limit outbound access wher appropriate.
  * Implement secure connectivity to on-premises networks.
* Compute - Secures access to VMs
  * Implement endpoint protection on devices and keep systems patched and current.
* Application - Ensures applications are free of security vulnerabilities.
  * Ensure that applications are secure and free of vulnerabilities.
  * Store sensitive application secrets in a secure storage medium.
  * Make security design a requirement for all application development.
* Data - Controls access to business and customer data.
  * Stored in a database.
  * Stored on disk inside virtual machines.
  * Stored in software as a service (SaaS) applications, such as O365.
  * Managed through cloud storage.

### Describe the purpose of Microsoft Defender for Cloud

Defender for Cloud monitors cloud, on-prem, hybrid, and multi-cloud environments. Defender for Cloud helps detect threats across:

* Azure PaaS services
* Azure data services
* Networks

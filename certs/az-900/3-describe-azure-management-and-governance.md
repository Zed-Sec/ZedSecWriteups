# 3 - Describe Azure Management and Governance

## Describe cost management in Azure

### Describe factors that can affect costs in Azure

There are many factors that impact cost in Azure, some of them are:

* Resource type
  * Settings
  * Azure region
* Consumption
* Maintenance
  * Using Resource Groups keeps things organized, which helps to deprovision resources that aren't needed anymore.
* Geography
* Network traffic
  * For data leaving the boundaries of an Azure datacentre, different areas are priced into data zones.
* Subscription type
* Azure Marketplace

### Compare the Pricing calculator and the Total Cost of Ownership (TCO) calculator

#### Pricing calculator

Gives an estimation of provisioning resoures in Azure. You can get an estimate for an individual resource or a fully built out solution.

#### TCO calculator

Designed to help compare the costs of running an on-premises infrastructure versus an Azure Cloud infrastructure. Compares the costs of your current infrastructure with the costs of an Azure environment supporting the same requirements.

### Describe the Azure Cost Management and Billing tool

Cost Management allows you to quickly check Azure resource costs, create alerts based on resource spends, amd create budgets that can be used to automate management of resources.

### Describe the purpose of tags

Tag provide extra metadata attached to resources. This can be used for:

* Resource management - associate tags with specific workloads, enviornments, business units, owner.
* Cost management and optimization - Group resources that you want to report on costs with.
* Operations managment - Allows you to group resources on how critical their availability is to your ogranization.
* Security tags - Can mark a resource by it's data level, public or confidential.

Tags consist of a Name/Value pair.

## Describe features and tools in Azure governance and compliance

### Describe the purpose of Azure Blueprints

When the scope of your cloud starts to expand past multiple subscriptions it's important to be able to apply a consistent set of policies an the new subscriptions. Azure Blueprints help you standarise cloud subscription or environment deployments.

Each component the blueprint definition is known as an artifact. Azure Blueprints dpeloy a new environment based on all of the requirements, settings, and configurations of the associated artifacts. Artifacts can include:

* Role assignments
* Policy assignments
* Azure Resource Manager templates
* Resource groups

### Describe the purpose of Azure Policy

Azure policy allows you to remain compliant and be alerted if the configuration of a resource has changes. Azure Policy allows you to create, assign, and mang

### Describe the purpose of resource locks

Resource locking prevents accidental deletion or editing of resources. There are two types of resource locks:

* Delete means authorized users can still read and modify a resource, but they can't delete th resource.
* ReadOnly means authorized users can read a resource, but they can't delete or update the resource.

### Describe the purpose of the Service Trust Portal

The Service Trust portal provides access to various resources about Microsoft security, privacy, and compliance practices. The portal gives informationa bout Microsoft processes, controls and compliance.

## Describe features and tools for managing and deploying Azure resources

### Describe the Azure portal

The Azure portal is the GUI portal that allows you to interact with Azure.

### Describe Azure Cloud Shell, including Azure CLI and Azure PowerShell

#### Azure Cloud Shell

A browser-based shell that allows you to create, configure, and manage Azure resources using a shell. Supports PowerShell and Azure CLI which is a Bash shell.

Cloud Shell is accessed via the Azure portal.

#### Azure PowerShell

A shell which can be used to automate repeatable tasks.

#### Azure CLI

Azure CLI is functionally equivalent to Azure PowerShell except it runs Bash commands as opposed to PowerShell commands.

### Describe the purpose of Azure Arc

Azure Arc lets you extend Azure compliance and monitoring to your hybrid and multi-cloud configurations.

Azure Arc allows you to:

* Manage your entire environment together by projecting your existing non-Azure resources into ARM.
* Manage multi-cloud and hybrid VMs, Kubernetes clusters, and databases as if they are running in Azure.
* Use familiar Azure services and management capabilities, regardless of where they live.
* Continue using traditional ITOps while introducing DevOps practives to support new cloud and native patterns in your environment.
* Configure custom locations as an abstraction layer on top of Azure Arc-enabled Kubernetes clusters and cluseter extensions.

### Describe Azure Resource Manager and Azure Resource Manager templates (ARM templates)

#### ARM

ARM is the deployment and management service for Azure. It allows you to create, update and delete resources in your Azure account. Anytime you do anything with your Azure resources, ARM is involved.

With ARM, you can:

* Manage your infrastructure through declarative templates rather than scripts. An ARM template uses a JSON file that defines that you want to deploy.
* Deploy, manage, and monitor all the resources for your solution as a group, rather than individual management.
* Re-deploy your solution throughout the development life-cycle and have confidence your resources are deployed in a consistent state.
* Define the dependancies between resources, so they're deployed in the correct order.
* Apply access control to all services because RBAC is natively integrated into the management platform.
* Apply tags to resources to logically organize all the resources in your subscription.
* Clarify your ogranization's billing by viewing costs for a group of resources that share the same tag.

#### ARM templates

Infrastructure as code is when you manage your infastructure using lines of code. ARM templates are an example of this. With an ARM template, you define the resources you want to use using a JSON file. With ARM templates, the JSON is verified before any code is run.

Benefits of ARM templates:

* Delarative syntax - Allows to declare what you want to deploy but you don't have to write the actual syntax commands to deploy the resources.
* Repeatable results - Repeatedly deploy your infrastructure throughout the development lifecycle, this allows resources to be deployed in a consistent manner.
* Orchestration - You don't have to worry about the complexities of ordering operations. ARM orchestrates the deployment of independent resources, deploying them in the correct order.
* Modular files - Templates can be broken into smaller, modular files that can be re-used in other deployments.
* Extensibility - You can add PowerShell or Bash scripts to your template, which extends functionality of deployments.

## Describe monitoring tools in Azure

### Describe the purpose of Azure Advisor

Azure Advisor evaluates Azure resources and makes recommendations to help improve reliability, security, and performance, achieve operational exellence, and reduce costs. Recommendation are provided and give advice on actions you can take right away, postpone, or dismiss.

When you're in the Azure portal, the Advisor dashboard displays recommendations for all your subscriptions. recommendations are diviced into five categories:

* Reliability - Ensure continuity of your business-critical applications.
* Security - Used to detect threats and vulnerabilities.
* Performance - Used to improve the speed of your applications.
* Operational Excellence - Used to help achieve process and workflow efficiency, resource manageability, and deployment best practices.
* Cost - Used to optimize and reduce Azure spending.

### Describe Azure Service Health

Helps keep track of Azure resources. This comes in three different services:

* Azure Status - Broad picture of the status of Azure globally. Informs you of service outages.
* Service Health - Narrower view of services and regions. Focuses only on the services and regions that you're using. This is helpful for looking for comms about outages, planned maintenance activities, and other health advisories because of the authenticated Service Health. You can set up notifications for planned maintenance and other changes that may affect your services and regions.
* Resource Health - Tailored view of your actual Azure resources. Giving specific information such as a specific virtual machine instance.

### Describe Azure Monitor, including Log Analytics, Azure Monitor alerts, and Application Insights

#### Azure Monitor

Platform for collecting data on your resources, analyzing that data, visualizing the information, and even acting on the results.

![AzureMonitor](https://learn.microsoft.com/en-gb/training/wwl-azure/describe-monitoring-tools-azure/media/azure-monitor-overview-614cd2fd.svg)

#### Azure Log Analytics

Lets you write log queries based ond ata gathered by Azure Monitor.

#### Azure Monitor Alerts

Automated way to stay informed when Azure Monitor thresholds are being crossed. You set the alert conditions, the notification actions, and then Azure Monitor Alerts notifies when an alert is triggered. Azure Monitor is also able to be configured to attempt corrective action.

#### Application Insights

An Azure Monitor feature, monitors your web applications. Capable of monitoring applications that are running in Azure, on-premises, or in a different cloud environment.

This can be configured with installing an SDK in your applications or using an Application Insights Agent. Application Insights is supported in C#, .NET, VB.NET, Java, JavaScript, Node.js, and Python.

When Application Insights is up and running you can monitor an array of information:

* Request rates, response times, and failure rates.
* Dependency rates, response times, and failure rates, to show whether external services are slowing down performance.
* Page views and load performance reported by users' browsers.
* AJAX calls from web pages, including rates, response times, and failure rates.
* User and session counts.
* Performance counters from Windows or Linux serv machines, such as CPU, memory, and network usage.

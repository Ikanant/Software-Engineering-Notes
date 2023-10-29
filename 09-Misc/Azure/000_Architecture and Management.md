Architecture and Management

Wednesday, March 9, 2022

10:47 PM

 

[THE BIG PICTURE]{.underline}

 

Azure is ultimately just a bunch of physical datacenters full of physical servers spread across the world. These are essentially organized into regions and availability zones, which are then organized using **Azure Resource Groups** (Logical containers that customer\'s servers, applications, customer data and services are grouped into)... this groups make the process of deployment and applying security way easier.

 

All Resources created in Azure are managed by **Azure Resource Manager** (Also known for it\'s acronym ARM). This is just a common management layer that is access by a variety of tools like:

-   Azure Portal

-   Azure PowerShell

-   Azure CLI

-   REST interface

 

Then there are the **Resource Manager Templates** which enable IaC (Infrastructure as code) which is a hot topic in the industry. This will allow us to script out repeatable deployment of our servers and application\'s infrastructure.

 

Last but not least, there is **Azure Advisor**, which is a built in tool that tells me how to optimize Azure for security best practices as well as cost-savings... which is nice in case we have people with limited knowledge with Azure.

 

[REGIONS AND AVAILABLITY ZONES]{.underline}

 

![.9 Azure - Physical Deployment Azure Regions High Availability Azure Geographies Availability Zones Disaster Recovery Region Pairs ](000_Architecture_and_Management_000.png){width="5.0in" height="2.783333333333333in"}

 

\*Every time we create a new Azure service we will be needing to specify the Location in which we wish to store our content... (There are some services that are considered global services though \-\--\> Like *Azure Active Directory Tenant)*

 

A region is the physical location of the DataCenter... there is a long list available to choose from... Even though they are all accessible through the internet we have to remember there is a performance element to getting our content. If most of my users are in the United States, it makes no sense to store my data in Australia. It\'d be slow!

 

*One thing to consider though it\'s that NOT all Azure services are available in all regions... so sometimes we do have to be creative with where we place our service if we wish to get access to a specific Azure service.*

 

*Check out:* <https://azure.microsoft.com/en-us/global-infrastructure/services>

 

A **Geography** can be a single country OR a set of countries. Within a Geography there are often Region pairs available. These are datacenters that are usually located 300 miles apart or more to reduce the impact on availability that might be caused by a natural disaster or major power outage. These can be very easy to use for automatic replication and failover. These pairs ALSO help with having *high availability* in the case we are running an update in one of our services... Azure makes sure that only ONE region in the pair is updated at one time... and if an outage affects multiple regions, at least one region in each pair will be prioritized for disaster recovery.

 

![Azure Geography Azure Region Availability Zone Availability Zone Availability Zone Azure Region ](000_Architecture_and_Management_001.png){width="5.0in" height="2.425in"}

 

*Availability Zones: Unique physical locations within a single region. They are made up of one or more data centers equipped with independent power, cooling and networking. These are not available in every region... but they ARE available, there is a minimum of THREE separate zones.*

 

 

[RESOURCE GROUPS]{.underline}

 

A Resource is simply a manageable item in Azure:\
 

-   Virtual Machines

-   Storage Accounts

-   Web Apps

-   Database

-   Virtual Networks

-   ...

 

A Resource group on the other hand is a container that holds resources.

![Resource Group Virtual Machines Databases Storage Accounts VNETs ](000_Architecture_and_Management_002.png){width="5.0in" height="3.066666666666667in"}

 

The important thing to note is that Resource groups have a set of resources **that share the same life cycle.** We deploy, update and delete them TOGETHER.

 

Each Resource we provision can ONLY exist in **ONE** resource group. They can be moved as needed though.

 

A Resource in Resource Group A can communicate with another Resource in Resource Group B.

 

One of the main benefits of having Resource Groups is that we can apply security controls to it for administrative actions.

 

*We can export IaC using Resource Manager Templates*

 

A Resource Group is just a container though for Resources. It is metadata with information about the Resources that it contains. Resource A, which lives in Region A, can be in the same group as Resource B, which lives in Region B. Likewise, a Resource Group can be created with Resources that live in a different Region.

 

*Deleting a Resource Group will mean you delete all of the Resources inside of it too.*

 

Funny enough, a Resource Group is also consider a Resource in Azure.

 

 

[AZURE RESOURCE MANAGER (ARM) and Management Tools]{.underline}

 

ARM is the deployment and management central for Azure. It is central for all the creation, deletion and modification of Resources that we do in Azure. The Azure portal is essentially just a website that sends request to the ARM end-points. ARM handles authentication using AAD (Azure Active Directory) and authorizes that you can perform actions that you\'re attempting to run.

 

Azure Portal is not the only way to send commands to manage Azure Resources though... This can be done using Powershell OR the Azure CLI. Azure also offers the Azure SDK for various programming languages that ALSO allow devs to build up their own tools to get changes up the Azure chain.

 

 

[AZURE CLI]{.underline}

 

I am going to choose to work with the Azure CLI from my Mac terminal. Seems straight forward.

1.  *brew update && brew install azure-cli*

2.  az \--version

3.  Az login

    a.  This will prompt browser to login

4.  az resource list

    a.  Test command to see if we are working.

    b.  Results will come in a JSON format

    ```{=html}
    <!-- -->
    ```
    c.  az resource list \--resource-group \[NameOfGroup\] \--out table

        i.  The \--out table will make things look nicer

![• Install the Azure CLI for Windowj X My Dashboard (2) - Microsoft A: X Overview of the Azure Micr X + ---s\' C aa-4c13-8940-c2c2dek P Search resources services and docs (G+/) Microsoft Azure My Dashboard (2) + Z ö \[b O O Create a resource H«ne Dashboard All services FMRITES (C) Resource groups Azure Active Directory Powersnell v Connecting termi • Welccne to Azure Cloud Shell Type \"az\" to use Azure CLI Auto refresh : Off UTC Time : 24 Type \"help\" to learn about Cloud Shell t•OTD: Cmdlet help is available: help \<cmdlet nne\> VERBOSE: Authenticating to Azure VERBOSE: Building your Azure drive \... PS /hcme/neil\> ](000_Architecture_and_Management_003.png){width="5.0in" height="4.033333333333333in"}

 

Worth noting I can use the Azure CLI or Powershell straight from the browser though. This is powerful in case I need to run some commands away from a computer with Azure installed.

 

Course is now going to show how to create a new resource BUT, he just mentioned something about **App Service Plan** (We are creating a simple web app)... The plan just defines the underlying infrastructure the app runs on... We define things like processing power needed for this resource AS WELL as where the price is set for the Resource.

 

Create plan:

 

![az appservice plan create - -resource-group NewTestRG - -nane TestAppSvcPIan \--sku SI ](000_Architecture_and_Management_004.png){width="5.0in" height="0.325in"}

 

THEN, create webApp:\
 

![uełd\-- dnoug-axłnosau- - ddeqaM ze ](000_Architecture_and_Management_005.png){width="5.0in" height="0.24166666666666667in"}

 

 

[RESOURCE MANAGEMENT TEMPLATES (Here\'s where IaC starts)]{.underline}

 

To implement things, Azure utilizes simple JSON files to define the infrastructure and configuration for the Resources we need to setup. It uses a declarative syntax so it is pretty straight forward to list what we want in our resources without having to write commands to actually get them done.

 

Templates can be deployed in a variety of ways... Azure Pipelines (CI/CD) is one of them. This is a part of as service called Azure DevOps (what I am really looking forward to work on)... Templates can ALSO be deployed from within GitHub AND powershell/AZ CLI.

 

Since the routes mentioned above use the Azure Resource Manager (ARM) REST API... it is also possible to run these through the API ... which also means I can deploy the templates straight from the Azure Portal.

 

Instead of writing templates from scratch, a neat trick is to just export existing configurations and see how the JSON files look in the end. This is what the DEMO in the Pluralsight course decides to do to save some time.

 

![-+- Add Edit columns Subscription (change) Visual Studio Professional Subscription ID -z all Delete resource group Oef1dba3-743c-4fe2-97bf-8d81c3e64c20 Refresh Move v Export to CSV Deployments No deployments +7 Add filter Type App Service plan App Service Open query e Assign tags Delete Export template Feedback View as ISON Tags (change) Click here to add tags Essentials Showing 1 to 2 of 2 records. Name TestAppSvcPlan webappnmcli Type = = all X Location --- Show hidden types @ X Location Canada Central Canada Central ](000_Architecture_and_Management_006.png){width="5.0in" height="2.2583333333333333in"}

 

 

[SERVICE HEALTH]{.underline}

 

Azure Service Health is available in the Portal. IN the Home page we can see the health of ALL of our Azure services across all regions. This comes from a separate service in Azure called Azure Status...

 

Taking a look into Health Advisories is cool. Essentially it list out any changes in Azure services that require my attention. For example, if a feature I use is being deprecated or I need to upgrade web application due to framework is being updated.

 

Security Advisories are similar... but these are going to be a list of violations that might affect our Azure services.

 

Here we can also setup alerts of any issues we might be dealing with. Alerts get sent to Action Groups.

 

**Azure Monitor**\
Is a solution for collecting and analyzing telemetry in our service. (Can even be setup to monitor ON PREM resources!) Basically this service is always collection data from our resources. This detailed monitoring applies to individual resources though NOT resource groups. Logs here are very useful.

 

Always worth noting that LOGS are events that happen within a system. They are typically not regular observations based on something happening, whereas METRICS are numerical values that describe a system at a particular point in time.

 

 

[AZURE ADVISOR]{.underline}

 

Microsoft refers to it as a personalized cloud consultant that helps you optimize your performance/availability/security of your Azure resources... as well as recommending ways that we can save cost in Azure. (Weird how you\'d think they want you to spend more money).

 

![All services Advisor Overview Recommendations Cost Security Reliability R Operational Excellence Performance All recommendations Monitoring Alerts (Preview) Recommendation digests Settings configuration Feedback Download as CSV Download as PDF o Your recommendations have been loaded Subscriptions: Visual Studio Professional --- Don\'t see a subscription? Open Directory + Subscription settings Cost You are following all of our cost recommendations See list of cost recommendations Security 13 Recommendations High 5 impact Medium 6 2 impact impact 10 Impacted resources ](000_Architecture_and_Management_007.png){width="5.0in" height="3.158333333333333in"}

 

The reports that we get here can easily be downloaded in a PDF or CSV file for various purposes and everything is pretty much broken down into:\
 

-   Cost

-   Security

-   Reliability

-   Operational Excellence

-   Performance

 

We can easily filter by which service we an to optimize AND we can postpone or dismiss certain recommendations if we wanted too.

 

One of the classic examples of people spending too much money in Azure is through the capacity of provisioned services (Life VMs) that might be under-utilized.

 

Depending on the type of issue identified, some things can be AUTO fixed by Azure. Like for example we get a warning that we have not disabled HTTP.

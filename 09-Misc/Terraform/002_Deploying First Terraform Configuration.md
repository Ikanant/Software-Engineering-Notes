Deploying First Terraform Configuration

Wednesday, January 5, 2022

11:45 PM

 

**What is Terraform?**

A tool to automate deployment and management of Infrastructure. Considering Infrastructure as any layer of technology a developer consumes without having to deploy and consume without having to deploy it.

 

It is an open-source project **maintained** by HashiCorp. It doesn\'t prefer any particular vendor so it can be used across anything like: AWS, Azure, DigitalOcean, VMWare, etc...

 

Core software is a simple binary compiled from GO. Hashicorp offers these binaries.

 

Terraform configuration files use declarative syntax. We describe how we want the world to be and Terraform does the heavy lifting.

 

Configuration files are written in Hashicorp configuration language (a derivative of JSON) or in JSON directly.

 

Terraform uses a push style of deployment to create the infrastructure. Terraform will reachout the API for any given service for any given service and tell it what to create. No agent to install on a remote machine.

 

 

**THERE ARE 4 MAIN COMPONENTS IN TERRAFORM:**

1.  Executable itself

    a.  This is the binary file we invoke to run Terraform. It contains all the core functionality needed to run the program.

2.  Configuration files

    a.  It could be stored on one of more of these files

    b.  Typically have the file extension .tf

    c.  When terraform sees this in a directory ... it will take them all and stitch them together into a Configuration

3.  Provider Plugins

    a.  This is what terraform uses to communicate with the services APIs

    b.  This is an executable

    c.  For instance AWS would be considered a provider... and if Terraform needs to communicate with it, it uses a provider plugin to do so

    d.  The most common plugins are hosted on the public Terraform registry at:\
        registry.terraform.io

4.  State data

    a.  This is what Terraform uses to keep track of what is going on.

    b.  Mapping of what we have defined in the configuration to what actually exists in the Target environment.

 

This is an extremely high level view of the DEMO application the course is going to work on to setup a very simple web application in a AWS environment:\
 

![Deployment Architecture Subnet-I VPC ](002_Deploying_First_Terraform_Configuration_000.png)

*The image above is a bit vague... so from the course I noted:*

1.  *Orange Layer: AWS-US-EST1 REGION*

2.  *Purple Layer: Creating a Virtual Private Cloud (VPC)*

3.  *Blue Layer: We are going to create a SINGLE subnet inside the VPC*

4.  *Icon: Single EC2 instance that is running NGNIX as a web-server*

5.  *\>\>\> Later in the config we will also have to setup ROUTING resources and a SECURITY group to [allow]{.underline} web traffic to reach that web-server*

 

Quick AWS EC2 summary to refresh my mind:

When running any application online we are always going to need servers... the problem is that we dunno how many will we need all the time. Sometimes we might need a few and sometimes we might need A LOT. Obtaining servers can be time consuming... we need to do research about what to buy, get budget approval and the purchase whatever we need. Once we do this we are stuck with it. Amazon Elastic Compute Cloud (EC2) makes it easy to obtain compute instances in the cloud.

 

When using Aws EC2, we simply select the template we want to use (Windows, Linux, etc)... and launch the quantity we need. We can do this using the online AWS management console OR automate the process using an API with whatever tool you want to use (AHHHA... this is where Terraform comes play)

 

Security is important, and with EC2 we have a few options to get those ready out of the box... Your application instances are always going to be located in a Virtual Private Cloud (VPC) that it is logically isolated network only WE control. Using a VPC allows us to use: **Network ACLs, AWS IAM users and permissions, Security Groups.** We can also connect to the data center through a separate hardware-based vpn device. If my application needs permanent storage, Amazon offers easy access to Amazon Elastic Block Store (EBS) to provide the persistent storage for the Amazon EC2 instance.

 

One great sale factor for EC2 is that it also provides with auto-scaling... in case things get rowdy in our application.

 

**Terraform Object Types**

-   Providers

    -   Defines information about a provider we want to use. That could be an Azure provider OR an AWS provider for example. It will also include basic information about the provide like REGION and/or ACCOUNT we will be using.

-   Resources

    -   Things we want to create in a target environment. They are the bulk of what we will be writing. Each resource is associated with a provider and typically requires some additional configuration for configuration.

        -   Examples can be: EC2 instance, Virtual Network or even a Database

-   Data Sources

    -   Way to QUERY information from a provider. We aren't creating anything... just asking for information we might want to use. Same as Resources Data sources are associated with a provider

        -   Examples can be: List of availability zones in a region, an AMI for an EC2 instance or a list of template on a cluster.

 

The Hashicorp configuration language uses blocks for EVERYTHING in the file. It\'s a simplified version of JSON that\'s easier to read AND supports inline comments.

 

Each block starts with BLOCK TYPE that describes the object that\'s about to be described

 

![block \_ type \"label\" = \"value\" key nested_block { key = \"value\' \' name \_ label \" ](002_Deploying_First_Terraform_Configuration_001.png)

 

This is a bit abstract so here is a better example when creating an EC2 instance on AWS:

 

Keep in mind that for the type of resource we are dealing with (an EC2 instance) based on the documentation from AWS provider, uses the label \"aws_instance\"

 

\"web_server\" is the name label for our instance. This gives us a way to refer to it... important if we have multiple EC2 instances.

 

![laws \_ instance\" \"web \_ server resource name = \"web -server ebs_volume { size = 40 ](002_Deploying_First_Terraform_Configuration_002.png)

 

**One important syntax to remember** is having the ability to reference other objects inside of a Terraform configuration... ACL has a defined configuration for doing so:\
 

**\<resource_type\>.\<name_label\>.\<attribute\>**

 

If we want the whole resource you can skip the attribute. For example, if somewhere else in my configuration I want to reference the name of my web server... I\'d just type: **aws_instance.web_server.name**

 

Currently I am going over the main.tf file provided by Pluralsight and one important thing they note is that ... we technically might have a hard time to figure out what parameters we can grab from other resources we define... for it the short answer is that we would need to read the documentation for the given provider we are using:

 

![](002_Deploying_First_Terraform_Configuration_003.png)

 

**[I really should re-watch the Reviewing the Base Configuration section of the course]{.underline}**

 

**Terraform Workflow:**

As mentioned multiple times at this point, Terraform uses provider plugins to interact with services. Before it can use those plugins, it technically needs to get them. This is part of the initialization process. The command for it is:\
 

***\> terraform init***

 

This command will look for configuration files inside of the current directory and examine it to check if it needs ANY provider plugins... if they do it will try to download them from the public Terraform registry (unless we specify an alternate location)... Terraform will ALSO need to store state data about the configuration somewhere. Part of the initialization process is to get a state data backend ready. If we don\'t specify and backend, Terraform will create a state data file in the current working directory. Once the initialization is complete, terraform is ready to deploy some infrastructure.

 

***\> terraform plan***

 

In this case Terraform will take a look at your current configuration, the content of your state data and determine the difference between the two... and THEN make a plan to update the target environment to match the desired configuration. Terraform WILL PRINT THE PLAN for us to look at in order to verify all is well. You don\'t HAVE to run terraform plan. You can save the plan changes to a file and then feed that back to terraform in the next step.

 

***\> terraform apply***

 

Assuming we ran the Terraform plan and save the changes to a file, Terraform will just execute the changes using the provider plugins. The resources will be created or modified and the state data will get updated to reflect the changes. If we run this again, terraform will say no changes are necessary and it will just hang in there for us.

 

***\> terraform destroy***

 

This is of course not necessary at all in many cases... BUT if we are done with the environment, the command destroy will literally do that. Destroy everything that is in the target environment BASED on what\'s on the state data. This is a dangerous command!

 

I will be using this command to save money when using AWS... but in the future, be careful!

 

![o ](002_Deploying_First_Terraform_Configuration_004.png)

 

 

**Summary:**

-   Terraform is infrastructure automation

-   Single binary for almost any OS

-   Configurations in JSON or HCL

-   Basic workflow: init, plan and apply

 

 

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

BONUS NOTES FROM THE BREAKDOWN OF THE MAIN.TF FILE IN Class:\
**Reviewing The Base Configuration\
**\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

 

 

>  

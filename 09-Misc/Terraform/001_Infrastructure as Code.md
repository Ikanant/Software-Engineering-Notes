Infrastructure as Code

Wednesday, January 5, 2022

11:18 PM

 

**What is it?**

As the name suggests, IaC is the process of provisioning infrastructure through **software** to achieve **consistent** and **predictable** deployments.

 

The goal for it really is to achieve consistency. This can easily get out of hand when done manually over time. The environment we get at the end is a PREDICTABLE environment. This is very important when we start trying to get MULTIPLE environments that need to run the same version of an application.

 

**Core Concepts:**

-   Defined in code

    -   We are going to be creating files to define the infrastructure. JSON, YAML or Hashicorp will be options

-   Stored in Source Control

    -   Will provide versioning and changelog history

-   There are two different approaches for implementing IaC:

    -   Declarative

        -   Relevant when we are dealing with software that already has some sort of implementation behind the scenes for accomplishing the task at hand. We can provide elements needed for a given task, but we don\'t need to specify the HOW to get it done.
        -   We are **declaring** what we want... and then we are leaving up to the software to figure out how to implement what we want.
        -   **[Terraform uses a declarative approach to deploying IaC]{.underline}**

    -   Imperative
        -   Describe **exact** steps to be reproduced

-   Idempotent and Consistent
    -   Recall that idempotency means: Property of a certain operation that can be applied multiple times without changing the result beyond the initial application. Meaning that re-running the same piece of code is not going change/re-add anything unnecessary.
    -   Terraform tries to be idempotent by NOT changing the environment it is creating/updating if no changes have been made to the configuration

-   Push or Pull
    -   Push: I have a resource and when I get a request for it I provide it
    -   Pull: Someone wants my resource and comes to me to get it
    -   Terraform uses a Push model
        -   The configuration that Terraform has will get PUSHED to the target environment.
        -   A pull configuration (NOT TERRAFORM RELATED) would be if we have an agent software running on an environment who pulls configurations from the central source on a regular basis

>  

**What are the benefits of IaC?**

-   Automated deployment. Faster Stronger
-   Created repeatable process
-   Consistent Environments
-   Documented Architecture

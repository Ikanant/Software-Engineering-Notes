Deep Dive

Sunday, August 25, 2019

7:58 PM

**From the Lerna official site:**

Lerna is a tool that allows you to maintain **MULTIPLE** npm packages within **ONE** repository. This paradigm is knows as a **monorepo.**

**Things to note:**

-   Pros

    -   Single lint, build, test and release process

    -   Easy to coordinate changes across modules

    -   Single place to report issues

    -   Easier setup of development environment

    -   Tests across modules are run together which finds bugs that touch multiple modules easier

-   Cons:

    -   Codebase looks more intimidating

    -   Repo is bigger in size

    -   Can\'t **npm install** modules directly from GitHub

    -   ??? Etc

**Who uses this?!**

React, Meteor, Ember, etc...

>  
>
>  

**How do we get started?**

-   \<npm install -g lerna\>

    -   This will install lerna globally on your machine

-   \<lerna \--version\>

    -   Simple way to make sure things were installed properly

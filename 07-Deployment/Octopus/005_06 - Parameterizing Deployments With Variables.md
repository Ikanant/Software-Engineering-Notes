06 - Parameterizing Deployments With Variables

Friday, November 18, 2016

11:15 AM

![](005_06_-_Parameterizing_Deployments_With_Variables_000.png){width="6.0in" height="2.575in"}

 

 

**Build Variables vs. Deployment Variables**

 

Mixing both types of variables in the deployment variables is a common trap. But it is important we don\'t configure our application at built time. By configuring the application at deployment time we avoid having to re-build our binaries when we want to deploy the application to a different environment. It also insures that we store potential sensitive information such as connection string s in a single place with control access instead of in Source Control where potential of leak is way higher.

 

![](005_06_-_Parameterizing_Deployments_With_Variables_001.png){width="6.0in" height="3.2916666666666665in"}

 

 

 

![](005_06_-_Parameterizing_Deployments_With_Variables_002.png){width="6.0in" height="3.941666666666667in"}

 

We can easily create Variables in the VARIABLES tab in our Project. When creating a variable we can specify various elements to them (Environment, Role, Steps, Targets). This will allow us to have multiple variables with the same name that will apply to different projects:

 

![](005_06_-_Parameterizing_Deployments_With_Variables_003.png){width="6.0in" height="2.716666666666667in"}

 

Another thing that we can do is use another variable as a part of our new vvariable. Like this:

 

![](005_06_-_Parameterizing_Deployments_With_Variables_004.png){width="6.0in" height="1.7666666666666666in"}

 

Keep in mind we need to make sure we are using the proper syntax to accomplish this.

 

Now when we go to the STEP template for a certain process, we can specify values there based in our application. **Note:** When changing a variable or any other setting in the STEP template, we will need to do a RELEASE in order to see our changes.

 

![](005_06_-_Parameterizing_Deployments_With_Variables_005.png){width="6.0in" height="3.658333333333333in"}

 

 

After this we MOST again create a new RELEASE. Octopus Deploy will gather again the STEP templates and the Values of all variables so that the release will always execute in the same way. So... EVERY time we add, remove or edit a variable we need to create a new release to apply the new values.

 

**Note 2:** To store password we can check the SENSITIVE option to mask the variable.

 

**Note 3:** We can also mark the variables to ask for a value at deployment time. We just need to specify the prompt link

 

 

**Configuration Variables**

We have just seen how we can parameterize the steps in the Deployment process, another part we usually want to configure is the Application itself. Namely the values used in the Web.config and App.config files.

 

Octopus Deploy allow us two different ways for doing this:

 

1.  Configuration Transformations

    -   Note that when a package is created no transformations are executed. This is because Octopus delays this step until the package is deployed.

    -   By default Octopus Deploy looks for 2 transformation files:

        1.  Web or App.release.config

            1.  Result in the same transformation for all deployments regardless of the environment

        2.  Web or App.\<EnvironmentName\>.config

            1.  This will allow us to create specific settings for each environments. In general this is not recommended because it moves configurations into Source Control and will move us away from a Central Configuration Point

            2.  This is enabled by default

    -   Replace appSettings / connectionString

        -   If any of the key matches with the name of a Variable, it will replace the current variable with the value of the newly found variable.\
             

2.  In the video example, we know that the app.config file contains a variable name to determine the url set for our application... since we want the URL to be different for QA and Live environment, we just need to create two variables that MATCH the name of the variable in our app.config file. When we do a new Release, the application will replace whatever data is in the app.config file with the value found in our Octo Server environment. The two variables that we create need to also be set for different roles to make sure we don\'t overwrite the wrong Release.

 

 

**Variable Sets**

 

Sometimes we might have settings that expand more than one project. For this Octopus Depoy offers VARIABLE SETS.

 

A Variable Set is a group of variables that can be shared across multiple projects. We can import this into any project and re-use them. This allows us to make changes to all of our applications at once.

 

Variable Sets can easily be used in our previous example:

 

![](005_06_-_Parameterizing_Deployments_With_Variables_006.png){width="6.0in" height="4.5in"}

 

 

**Create Variable Sets**

 

1.  Go to the **Library** tab \> Variable Sets \> Add Variable set

    a.  Give the set a name and a description

2.  Now we can create Variables just as we did in the Project Variables

    a.  ![](005_06_-_Parameterizing_Deployments_With_Variables_007.png){width="6.0in" height="1.0833333333333333in"}

3.  Now that we have the Variable sets we can go to the Projects and include the variable sets from the Library

    a.  ![](005_06_-_Parameterizing_Deployments_With_Variables_008.png){width="6.0in" height="2.3583333333333334in"}

 

**Built-in System Variables**

 

![](005_06_-_Parameterizing_Deployments_With_Variables_009.png){width="6.0in" height="2.225in"}

 

 

In the case that we want to Debug and inspect the values of the Variables we are using in the Logs...we can just define two variables and set them as true in our setting:

 

![](005_06_-_Parameterizing_Deployments_With_Variables_010.png){width="6.0in" height="3.5083333333333333in"}

 

 

 

![](005_06_-_Parameterizing_Deployments_With_Variables_011.png){width="6.0in" height="3.1333333333333333in"}

 

 

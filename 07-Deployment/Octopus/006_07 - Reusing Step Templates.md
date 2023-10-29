07 - Reusing Step Templates

Friday, November 18, 2016

11:51 AM

 

By doing this we will make our deployment process more flexible.

 

Up until now we have only used a Deploy Package step in our DEMO application. Octopus Deploy provides us with several other steps to take.

 

We can also look into creating our own Step templates and also include various Templates used by the community.

 

![](006_07_-_Reusing_Step_Templates_000.png){width="6.0in" height="2.2416666666666667in"}

 

 

**Built-in Step types:**

 

1.  Deploy package

    a.  Deploys NuGet packages (as we have already seen)

    b.  Which also includes extra features which also allow us to deploy web apps and windows services.

    c.  JSON Configuration Variables

        i.  This will allow us to do the same variable substitution as we did with our web and app.config files.

        ii. The same can be done by enabling the feature Substitute Variables in Files for any file.

    d.  Custom Installation Directory

2.  We can also directly deploy applications to Azure for Cloud Services, Web Apps and Resource groups

3.  Run PowerShell scripts in the Azure tool enabled for full custom scripting on Azure.

4.  For notification we can have an EMAIL step that will use SMTP server

5.  Manual Intervention

    a.  Cause the deploy template to hold before continuing with the next steps. This is usually done in an approval workflow.

6.  Run a Custom Scripts as a STEP

 

 

**Creating Custom Step Templates**

 

A Step is commonly attached to the process of a project. If we want to re-use a Step we need to create a Step Template ourselves.

 

To do that:

1.  Library \> Step Templates \> Add

2.  Pick Step type:

    a.  Ex: Script Step

3.  Script that we are adding will invoke a URL to warm up our application.

    a.  Name it: Warm Up for example

    b.  If we look at the script we can see a variable called **\$address**. We can define parameters for our custom step and Octopus will pass in the values of this parameters as a variable to the custom script

4.  To Define Parameter

    a.  Head to the parameter tab

        i.  Provide Name and user friendly description and the type of Control needed.

5.  Save Template

6.  Head over to Our_Project \> Process \> Add a Step ... now we can see that there is an extra step available to be included

    a.  Because this STEP does NOT need to be executed on the Target machine I will tell it to execute on the Octopus Deploy Server (web-server)

    b.  Input to specify the Address To warm up our application:

        -   ![](006_07_-_Reusing_Step_Templates_001.png){width="6.0in" height="3.5416666666666665in"}

    c.  Instead of using a FIX value, we can use the variable we set in in the IIS bindings from before:

        i.  #{binding}

    d.  This will ensure that the warm up will be executed on the correct address

7.  AS usual, after modifying the process we need to create a new release.

8.  Once DONE we can go to the TASK log and we can see that our new Step has been executed.

9.  This STEP template can now be executed in many different projects.

 

**Import Step Templates**

 

If we look at the Custom Step we defined earlier, we can see that we can Export it. This is useful when we want to use the Step on a different Octopus Deploy Server. The export will generate a JSON file that will have all the information needed to recreate the STEP template on a different Server, such as the Script body and the parameters.

 

The same way we can export it, we can also IMPROT script Templates.

 

The Import Dialog allows us to PASTE in a JSON definition of the Script template. On the Site:

 

<https://library.octopusdeply.com/listing>

 

We can see a huge amount of Scripts created by the community.

 

![](006_07_-_Reusing_Step_Templates_002.png){width="6.0in" height="2.5166666666666666in"}

 

 

 

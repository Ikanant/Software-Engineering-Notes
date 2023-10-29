Using Input Variables and Outputs

Tuesday, January 18, 2022

8:02 PM

 

**Working with Data in Teraform**

Within Terraform we receive variables as input AND even change their values within configuration files.... AAAND even return their values.

 

**Variable Syntax looks something like:\
** 

![variable variable \'name \_ label\" \"name_label\" o value type = description = \"value\" default = \"value\" sensitive = true false ](003_Using_Input_Variables_and_Outputs_000.png)

 

If no argument is provided to a variable that is no problem. This is a simple and dirty way to define a variable in our configuration file that can be updated later on. When we do provide parameters to our variable we can setup the type (Data types to come), the description, the default value (Terraform will ask for it in the command line) AND whether or not we are dealing with sensitive data... this will defined if the Terminal/Console displays the value of this variable.

 

![variable \" aws_region\' type = string description = \"Region to use for AWS resources default = \"us-east-I Terraform Variable Reference var . var .aws_region ](003_Using_Input_Variables_and_Outputs_001.png)

 

**Data Types** can be sumarized in 3 categoires:\
 

1.  Primitive

    a.  String, number, boolean

2.  Collection (Need to be of the same type)

    a.  List

        i.  Considered an ordered group of elements

    b.  Set

        i.  An un-ordered group of elements

    c.  Map

        i.  Key Value Pairs

3.  Structural. Similar to collections but they allow to mix data types in each grouping.

    a.  Tuple

        i.  Equivalent to lists

    b.  Object

        i.  Equivalent to maps

 

 

![\# List \[ us-east-I\' us-east-2\", \"us-west-I \" , \[1, true\] \# INVALID LIST! us-east-2\" , medium = \"t2.sma11\" \# Map small = \"t2.micro\' ](003_Using_Input_Variables_and_Outputs_002.png)

 

Example of a LIST:

![variable \"aws_regions list (string) type = description = \"Region to use for AWS resources\' default = \'us-east-2\" , us-west-I us-east-I Collection Values ](003_Using_Input_Variables_and_Outputs_003.png)

 

Example of a MAP:

![\"aws_instance_sizes\" variable type = map(string description = \"Region to use for AWS resources\" default = small medium large = \"t2 . micro\" = \"t2 . small\" - \"t2.1arge\" ](003_Using_Input_Variables_and_Outputs_004.png)

 

**Now it is time to jump back to the code... in the example scenario from pervious notes there are quite a bit of places where using variables could be of high importance... For example, the AWS credentials put straight into the main.tf file is a big NO NO.**

 

![main.tf --- Getting-Started-Terraform variables.tf main.tf x globo_web_app \> main.tf \> provider \"avvs\" \> secret_key \# PROVIDERS provider \"aws•• access secret region \# DATA \_ key \_key = var. = var. = var. 11 12 13 14 15 aws_access_key aws_sec ret_key aws_reg Ion \" arni lø 11 12 13 14 15 varn varii varii data ](003_Using_Input_Variables_and_Outputs_005.png)

 

In my AWS instance I ended up creating the variables.tf file inside of the same directory as main.tf and this allowed me to store are the variable values there. Simple.

 

**Local Values Syntax**

As mentioned earlier, local values are computed inside the configuration.. Unlike input variables... the syntax starts with keyboard **local**

 

These will just be filled with key/value pairs... Simple!

 

![locals instance_prefix - common_tags - \" globo \" Globomantics company project = var. project billing \_ code = var. bill il Terraform Locals Refer ](003_Using_Input_Variables_and_Outputs_006.png)

 

![](003_Using_Input_Variables_and_Outputs_007.png)

 

Notice how in the example above we simply used locals to add simple tags to a few of the resources for the AWS instance. In this case we did NOT apply one to the **aws_route_table_association**... When using tags in the future we need to be careful and know which resources actually allow for the use of certain properties.\'

 

**Outputs Syntax**

Outputs values is the way we get values OUT of terraform. They will be displayed in the TERMINAL at the end of a configuration run. It exposes values when a configuration is placed inside a module (covered later).

 

In the syntax... the ONLY required argument is the **value** for the output.

 

Just like the value of a local, the value for an output can be any supported data type. Return a string or a complex object.

**Sensitive flag** works the same as before, it will just NOT display the value in the terminal. This seems weird to me because why would we care about it if it is not going to be displayed properly in the output? \-\-- this will be answered when I go over Modules.

 

![output \"name \_ label\" value output \_ value \"Description of description true I false sensitive - ](003_Using_Input_Variables_and_Outputs_008.png)

 

Example:\
 

![output \"public_dns_hostname\" value aws_instance . web \_ server . put \"Public DNS hostname description - ](003_Using_Input_Variables_and_Outputs_009.png)

 

![main.tf globo_web_app \> output variables.tf locals.tf globo_web_app \> outputs.tf \> c 28 29 31 32 33 main.tf \> = local. comon_tags tags \"igw•• { resource vpc_id = aws_vpc. vpc. id 1 2 3 output value = aws_instance.ng PROBLEMS OUTPUT DEBUG CONSOLE primary_network_interface_id private_dns rivate_ip btic_dn public_ip + secondary_private_ips + security_groups TERMINAL after after after after (known after apply) after after after ( known ( known ( known ( known ( known ( known (known apply) apply) apply) apply) apply) apply) apply) ](003_Using_Input_Variables_and_Outputs_010.png)

What\'s really important here is that the output value is actually not used at all in any of our main.tf files. When we apply a Terraform configuration file we see a good amount of parameters that have **(known after apply)** ... these parameters are the ones that can be real useful when printing stuff out to our terminal... In this case it is saving us a trip to AWS console to grab the public_dns value of our web server.

 

*Using the Terraform VS Code extension has made my life quite easier with their auto-complete and bad sytnax highlighting BUT... this is not 100% certain we have a valid configuration. That\'s where the VALIDATE step comes in.*

 

**Validate the Configuration**

 

Before we run the command we need to run **init** first. This is because it is checking the syntax and arguments of the resources in the providers and it needs the provider resources to do so. In other words, it needs a way to know which provider we use (like AWS resources) and handle the validation from there... AWS is different than Azure for example.

 

If it finds any errors it will print it in the console and SOMETIMES it might even print a suggestion... it DOES NOT check the current state of the deployment. It also does NOT guarantee that the deployment would be successful. Syntax and Logic might be great, but the deployment can still fail for many other reasons.... Like insufficient capacity or whatnot.

 

**Supplying Variable Values**

 

Everything noted until now is well and good, but HOW do we provide the value for the all the variables we have thrown into my project.... Turns out there are SIX ways of doing so.

 

1.  (Easiest) Set the value with a **default** argument

2.  At the command line when running **terraform run** with a flag like: **-var flag**

3.  Can have all the variable values in a file. Use the flag during **terraform run** as well. **-var-file flag**

4.  Automatically picked up file

    a.  If there is a file in the same directory as my configuration named **terraform.tfvars** or **terraform.tfvars.json** then Terraform will use the values found in this file

5.  If there is a file in the same directory as the configuration with:

    a.  **.auto.tfvars** or **.auto.tfvars.json**

    b.  Pretty much same as number 4

6.  Environment Variables

    a.  Terraform will look for ANY environment variables that **start with TF_VAR\_**

 

The important thing to note is that if we DO NOT submit a value using ANY of these ways for variables in the configuration, then Terraform will [prompt you]{.underline} for the value.

 

The OTHER important question to ask is, what happens if we define a value for a variable in multiple places? Well, time to memorize an order of precedence:

 

![TF VAR environment variable .tfvars or .tfvars.json .auto.tfvars or -var-file flag .auto.tfvars.json -var fl ](003_Using_Input_Variables_and_Outputs_011.png)

 

Terraform evaluates from left to right... so anything passed in the the Command line prompt for example will overwrite the TF_VAR\_ environment variable.

 

BOOM... DONEZZO\
\
 

![Overview fil Supply data through il Many ways to submit Receive data through ](003_Using_Input_Variables_and_Outputs_012.png)

 

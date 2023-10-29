Core Concepts

Saturday, February 11, 2023

3:52 PM

 

GitHub Actions enables us to create CUSTOM software development life cycle (SDLC) workflows... These action can listen when specific activities happen on GitHub, at a scheduled time OR when an event outside GitHub occurs. We no longer need to depend on external CI/CD integrations in order to add CI/CD capabilities to our git flow. The level of automation we get is pretty great out of the box.

 

**Dissection the Workflow File**

 

The workflow file lives at the root of the repo in the .github/workflows directory.

 

You CAN create more than workflow in a repository. These are just going to be yaml files in the workflows directory. The one thing to keep in mind is that the **name** is the first line in all of these files (not required). The name can be anything, we just need to try to make as descriptive as possible about what this Workflow is about....

 

![simple-workf ](000_Core_Concepts_000.png){width="3.8583333333333334in" height="1.0in"}

 

If no name is specified, then GitHub will use the file name.

 

The next part of the workflow file will define the WHEN the workflow will be triggered...

 

![2 3 4 5 6 on: push: branches: \[ mast pull \_ request: ](000_Core_Concepts_001.png){width="5.0in" height="2.716666666666667in"}

 

When an event occurs... such as a commit/merge/pr/when is created.... We can trigger this workflow. We can get quite specific with our triggers... above we see we are filtering our events with the branch name... but we can also do:\
 

![on: push: branches : - master tags: ](000_Core_Concepts_002.png){width="1.9583333333333333in" height="2.75in"}

 

Here we can see the trigger will happen ONLY when a PUSH gets done in a master branch BUT only for commits that are pushed for the **v1** tag... and also only files that are in the test directory.

 

Now that I defined when the workflow will be triggered, then I need to define what will actually happen. This is when we define our actions...

 

Actions: Are the individual tasks that we combine as steps to create a job:

 

![13 14 steps: --- uses: actions/checl ](000_Core_Concepts_003.png){width="5.0in" height="0.8416666666666667in"}

 

Actions are the SMALLEST portable building block of a workflow.

 

How about JOBS?

Workflows most have AT LEAST one job... jobs contains a set of steps with actions or run commands or even API calls that will execute when the workflow is triggered. Actions can be written from scratch or consumed from the GitHub community.

 

![9 10 11 12 13 14 15 16 18 19 jobs: build: runs---on: steps: --- uses: --- name: run: --- name: ubuntu---latest actions/checkout@v2 Run echo Run a one---line script Hello, world! a multi---line scrip ](000_Core_Concepts_004.png){width="5.0in" height="4.075in"}

 

Nested under Jobs in the code... it\'s the name of the defined job... meaning above we could have named **build** whatever we wanted.

 

Under the name definition we have **THE RUNNER**

 

![:jobs :build ](000_Core_Concepts_005.png){width="3.0416666666666665in" height="0.95in"}

 

A runner is ANY machine with the GitHub Actions runner application installed. These can be GitHub\'s own hosted runners OR self-hosted runners. These can run DIRECTLY on a machine OR in Docker containers.

 

On the **runs-on** we provide the runner\'s type OR the workflow label... In the example above we are just using a github hosted runner. These run in a FRESH instance of a virtual environment.

 

![Virtual environment Windows Server 2019 Ubuntu 18.04 Ubuntu 16.04 YAML workflow windows-latest ubuntu-latest or ubuntu-16 .04 ](000_Core_Concepts_006.png){width="5.0in" height="1.0833333333333333in"}

 

These are the available hosted runners (at least that I am aware off at the time of the recording of the training)

 

Self hosted runners offer WAY more flexibility for what to use of course.

 

![runs-on: \[self-hosted, linux ](000_Core_Concepts_007.png){width="5.0in" height="0.6583333333333333in"}

 

Self hosted runners gets the **self-hosted** label and each of them have labels for their OS and System Architecture.

 

![• self-hosted - Run this job on a self-hos • linux - Only use a Linux-based runner ](000_Core_Concepts_008.png){width="5.0in" height="0.7in"}

 

The next step is to go over the series of STEPS in the job...

 

![steps: --- uses: --- name: run: --- name: actions/checkout@v2 Run echo Run a one---line script Hello, world! a multi---line script ](000_Core_Concepts_009.png){width="5.0in" height="3.216666666666667in"}

 

These will all run under the same job and host machine... which allows each step to share info.

 

There are such a thing as STANDARD ACTIONS... for example:\
 

![: sdus ](000_Core_Concepts_010.png){width="5.0in" height="0.7916666666666666in"}

 

Check out is one of many. The standard checkout action is one that you MUST have in the workflow IF you have any step that requires a copy of the repo. This will checkout the repo under a folder called **Github-Workspace.**

 

NOT ALL STEPS RUN ACTIONS... BUT ALL ACTIONS RUN AS A STEP

 

We see this right next line in:\
 

![--- name: Run a one---line run: echo Hello, worlc ](000_Core_Concepts_011.png){width="5.0in" height="1.1583333333333334in"}

 

The name is something we define... but these are examples of simple scripts we can run in the host machine... it seems to already come with git ready to go... see example bellow (IT WORKS)\
\
 

![steps : --- uses: --- uses: naræ: with: actions/checkout@v3 actions/setup---node@v3 Use Node. js matrix. node---v node---version: matrix. node---ver cache: •npm• --- run: echo Helto World IRO --- run: I echo Hello World DOS echo Heno World TRES --- run: I ](000_Core_Concepts_012.png){width="4.0in" height="4.091666666666667in"}

 

EVENTS:

 

![n: pull-request \_ comment on: check \_ suite on: pull \_ delete request on: on: pull_request_rev ](000_Core_Concepts_013.png){width="5.0in" height="1.0916666666666666in"}

 

There are so many.... BUT mainly in three categories:

1.  Specific Activity on GitHub happens

    a.  Commits/PR(s)/Issues

    b.  These events are defined with the **on:** at the top of the file

    c.  These can be stacked... meaning you can do a **on: push** OR **on: \[push, pull_request\]**

    d.  ACTIVITY TYPES

        i.  Events can have their own types that will allow for a more granular approach to WHEN something gets triggered.

        ii. ![Webhook Event Payload pull \_ request Activity Types - assigned - unassigned - review_requ review_requ --- labeled - unlabeled Opened edited - closed ](000_Core_Concepts_014.png){width="5.0in" height="2.75in"}

        iii. By default ALL types will be trigger when we defined the event in our workflow

        iv. Otherwise we can just use the **types** keyboard under the event... i.e.:

        v.  ![on: pull \_ request : ](000_Core_Concepts_015.png){width="5.0in" height="1.2083333333333333in"}

        vi. <https://docs.github.com/en/developers/webhooks-and-events/events/github-event-types#pullrequestevent>

2.  Scheduled

    a.  CRON Syntax

    b.  These run on the LATEST commit on the default or base branch

    c.  Shortest time available is only ONCE every FIVE minutes

    d.  ![on: schedule : ](000_Core_Concepts_016.png){width="5.0in" height="1.5416666666666667in"}

    e.  ![minute (0 59) hour (0 23) day of the month (1 - 31) month (1 DEC) - 12 or JAN - day of the week (0 ](000_Core_Concepts_017.png){width="5.0in" height="1.95in"}

3.  Event outside of GitHub occurs

    a.  These are called when a WebHook event happens called **Repository Dispatch**

    b.  We would need to use the GitHub API for these

    c.  **Send a POST request to the GitHub API endpoint**

    d.  In order to use this though, we NEED a **repository_dispatch** with the identified type (gotta check if the type is required, I think so)

    e.  ![on: repository \_ dispatch types: \[opened, delc ](000_Core_Concepts_018.png){width="5.0in" height="1.2166666666666666in"}

>  

**ENVIRONMENT VARIABLES AND SECRETS**

 

To make a secret available to an action, we can set the secret as an INPUT or ENVIORNMENT VARIABLE in the eworkflow file.

 

Creating secrets is done in the **Settings** of the repository.

![\< \> Code G) Issues @ General Access AA Collaborators Q) Moderation options Code and automation P Branches Tags @ Actions Webhooks Environments 8 Codespaces t Pages Security Code security and analysis Deploy keys Secrets and variables Pull requests @ Actions Projects CD Wiki C) Security Actions secrets and variables I.E Insights Secrets and variables allow you to manage reusable configuration data. Sec s sensitive data. Learn more about encrypted secrets. Variables are shown as Iail sensitive data. Learn more about variables. Anyone with collaborator access to this repository can use these secrets a va passed to workflows that are triggered by a pull request from a fork. Secrets Variables Environment secrets There are no Repository secrets ts for this repository\'s nvironr There are no secrets for this repository. ](000_Core_Concepts_019.png){width="5.0in" height="3.7083333333333335in"}

 

To provide a value to our workflow in a secret or environment variable we can use the

![steps : name: Hello world with : super \_ secret: \${{ secrets. M) ](000_Core_Concepts_020.png){width="5.0in" height="2.2in"}

 

Some actions will require authorization as a secret input for example.

 

We can set the secret as an INPUT by using the **with:** tag OR as an ENVIRONMENT VARIABLE using the same format but with **env:**

 

**GITHUB_TOKEN**

This is a secret that is [automatically]{.underline} created to use in our workflows is the GITHUB_TOKEN. We do not need to define it. When we enable GitHub actions, GitHub installs a GitHub app into the repository. The token secret it\'s a github app installation access token that we can use to AUTHENTICATE on behave of the GitHub app installed on the repo.

 

The token\'s permissions are limited to the repo that contains the workflow. To use this secret we just need to provide it to the GitHub workflow file... We can pass it as an INPUT for an ACTION that requires it. We will use this to make authenticated GitHub API calls.

 

<https://github.com/actions/labeler>

 

Taking a look at the labler action for example...

![jobs: triage: runs-on: ubuntu-latest ste s: - uses: actions/labeler@v2 with : ](000_Core_Concepts_021.png){width="5.0in" height="1.825in"}

 

 

The action requires the GitHub_Token as a value of the repo-token input parameter.

 

On the other hand, let\'s say we want to perform an API call on the repo that we are on... For example, create an ISSUE for us... to do this we can make the curl POST request as so:

 

![](000_Core_Concepts_022.png){width="5.0in" height="2.4916666666666667in"}

 

 

**IN SUMMARY:**

 

![Actions are your units of code. You can use Act the marketplace one on your owr To use an action ](000_Core_Concepts_023.png){width="5.0in" height="2.908333333333333in"}

 

![1010 1110 1010 Artifacts are thc created when y and test your cc Binary, package files ](000_Core_Concepts_024.png){width="5.0in" height="2.908333333333333in"}

 

![Create cust01 workflows th building and code Create cust01 workflows to automaticall) code to any ](000_Core_Concepts_025.png){width="5.0in" height="2.908333333333333in"}

 

![Specific activiti trigger a workfl on: Provide a single array of events, ](000_Core_Concepts_026.png){width="5.0in" height="2.908333333333333in"}

 

![O This tells our wo where the virtua environment wil Wait for an avail to be kicked off event is triggere ](000_Core_Concepts_027.png){width="5.0in" height="2.908333333333333in"}

 

![A job consists of more steps Jobs can run independently o sequentially A step is a set oi ](000_Core_Concepts_028.png){width="5.0in" height="2.9166666666666665in"}

 

![An automated proce made up of one or and can be triggerec event Defined using a YAM . github/workflows ](000_Core_Concepts_029.png){width="5.0in" height="2.908333333333333in"}

 

![instance of that runs when configured eve You can see th actions, logs, a for each workfl ](000_Core_Concepts_030.png){width="5.0in" height="2.9166666666666665in"}

 

Introduction

Saturday, August 3, 2019

9:03 PM

These notes will not be focused on a list of git commands and their respective actions\... that\'s something that can be googled at any time. Instead, I plan to write down the key concepts that will make any dev understand the way that GIT works behinds the scenes which should allow us to become masters whether we are using the terminal / any tool out there for versioning our code.

![Git Commands git filter-branch git diff git ref log git commit git rerere git add git log git clean git bisect git help git pull git grep git git clone git status git merge git rebase rm git revert git push git remote git init git branch git cherry-pick git config ](000_Introduction_000.png)

Quick Note Reminder: In GIT, \"Origin\" is a shorthand name for the remote repository that a project was originally cloned from. In the following example, the URL parameter to the \"clone\" command becomes the \"origin\" for the cloned local repository:

The one thing to keep in mind when dealing with GIT, is that in each project there are 4 Storage AREAS\... and you move data across them.

**The FOUR Areas:**

1.  Working Area (Simply your project directory or your file system)

    a.  The place where we have our CURRENT files/folders

2.  Repository

    a.  Contains the entire history of the project. When we commit work, it goes here.

3.  Index (The Staging Area)

    a.  The place where we put our files before a COMMIT

4.  Stash

    a.  Temporary storage area

>  

![Stash Working Area Index Repository ](000_Introduction_001.png)

**IF we ever really want to understand the way that GIT works, we need to ask 2 important questions:**

1.  How does this command move data across these 4 areas?

2.  What does this command DO to the repository specifically?

>  

It doesn\'t matter how complex a command looks. If we are able to answer these 2 questions, we should be set.

**THE WORKING AREA**

This is where we work, we edit our files, test our code, etc\... For the most part GIT doesn\'t care much about our working area. For the most part this is not a place that GIT will try to destroy data as you work and should be in almost the full control of the user. There are some commands that can affect our work here though\... ONCE we commit our data, GIT stores it into what what it considers to be the REALLY important area.

**THE REPOSITORY**

The repository is in the .git folder. And the most important data is inside the folder .git/object.

There are a few different kind of objects in the DB. Some objects represent the content of a file at some point in the project history\... these objects are called **BLOBS.** There are other objects that are meant to represent folders in our repository called **TREES.** And lastly there are **COMMITS.** All of these objects are INMUTABLE\... they can be created/deleted BUT they can never be changed! These objects are linked together in order to compose our projects history:

![blob blob tree commit tree commi t tree blob ](000_Introduction_002.png)

Each commit points to a graph of blobs and trees that represents our files and folder at the point of each commit. SO each commit behaves as a snapshot of our working area.

EACH Commit is also pointing at its parent commit in the history. Commits that are chained together are a bunch of sequential snapshots that form slices of our project history. References to these commits are called BRANCHES.

Branches: A reference to a commit. Because a branch is reference to a commit, and because each commit is linked together to become its history the Branch is basically the ENTRY POINT of the history of a commit.

**The HEAD**

There is a special POINTER called the HEAD. There can be ONLY ONE HEAD\... and it\'s usually connected to a branch\... so a HEAD is pointed to a BRANCH which is pointed to a COMMIT

![branch2 HEAD commi t 1 commi t c 1 commit commit commi t commi t ](000_Introduction_003.png)

One important thing to note is that sometimes we make commits that cannot be reached from ANY branch. Think of it as if we deleted branch1 in the image above\... In these cases, GIT will delete them as it runs it\'s garbage collection process.

**THE INDEX**

Every source control tool out there has the concept of the Working Area and a Repository but the INDEX is unique to GIT. (Or at the very least the only versioning system that allows you to modify it directly).

The INDEX is something that is placed between the Working Area and the Repository. You can\'t move things directly from the Working Area to the Repository\... that is why the INDEX is also called **THE STAGING AREA.**

We STAGE the changes by adding them from the working area to the INDEX, and THEN we commit those changes from the INDEX to the repository

Let\'s say we are working with a checked out code in our local and we run the command **\<git status\>** if we didn\'t make any changes, we essentially will get a \'branch is up to date\' message. In this case we have the working area and the repo are aligned. [They contain the same stuff.] But something interesting is at play here, the files in our repo have been committed sometime in the past are in the REPOSITORY\... but when we say that things are ALIGNED, we mean that the files in our working area are equivalent at what the [current commit] in the repository. Of course the REPO will contain also other commits and other files\...

![Working Area menu. txt O recipes Index Repository menu. txt recipes 1 ](000_Introduction_004.png)

This is something that is not super important to keep in mind, but if we want to understand how GIT is managing things behind the scenes, it\'s worth noting it.

When thinking of the INDEX, most people (including myself here) think of the staging area as the transition area\...a launch pad of sort.. It is normally empty, we add files to it, we launch the files into the repo AND then the index is empty again\.... this is actually the way it is implemented\... but it is smart to think of it in a slightly different way\...

A better way to think of it just another area that holds EVERYTHING\... so when we say **\<git status\>** and we see the up to date msg\.... that does not mean that the INDEX is empty, it means that the index contains the same files and folders as the repo.

**\<git diff\>** will compare the files between the WORKING AREA and the INDEX

**\<git diff \--cached\>** will compare the files between the INDEX and the REPOSITORY

Basic Workflow

Sunday, August 4, 2019

12:44 PM

 

Looking into the most basic process in GIT\... let\'s say we have a repo with a file and we decide to edit\... once we do we perform a\
**\<git status\>** And we will see the change that we made and the fact that it has not yet been moved to the staging area.

 

**\<git add\>** When doing this the file has been copied from the Working Area to the Index.

 

**\<git diff\>** Now shows NO difference. The working area and the Staging area are the same

**\<git diff \--cached\>** Since this step compares what\'s in the Index area and the Repo, we do see the differences from our change.

 

**\<git commit\>** The updated file will get copied from the Index to the Repository.

 

Changes above we essentially move data from LEFT to RIGHT

 

One thing to notice is that our last **commit** command did MORE than just copy our file into the repository. It created a new commit other objects AND updated the current branch.

 

**Move data RIGHT to LEFT**

 

**\<git checkout\>** Checkout does TWO things:

1.  In the Repository, it MOVES the HEAD reference. Generally to another branch\... (changes the current commit)

2.  It takes data from the CURRENT COMMIT and it copies that data from the REPOSITORY to the WORKING AREA and the INDEX

>  

**\<git branch\>** Shows the available branches\...

 

**\<git diff myBranch master\>** Checks the differences between myBranch and the Master branch.

 

**\<git checkout myBranch\>** Keep in mind that the files that we had in the REPOSITORY, there was a COMMIT pointed to them\... These are the current commit because there is a branch pointed to it (In this case Master).. And then HEAD is pointed to this branch\... So the first thing that happens when we perform a checkout is that HEAD moves to the myBranch last commit.

 

The SECOND thing that checkout did is to COPY the current data from the REPOSITORY to both the WORKING AREA and the INDEX.

 

**REMOVING files in GIT**

 

What if I wanted to remove a file that I have already added to the Index (staging area)? - not hard delete the file, but instead just bring the file back to the original state before the **\<git add\>** command\...

 

**\<git rm myFile\>** ??? NOPE that would not be a good idea. Because Remove does a bit more than just un-staging our file\... it goes full on deleting it from both the Index AND our Working area. Good news is that git should give you a warning if we do this\... now if we do something like

 

**\<git rm \--cached myFile\>** this would then remove the file from the INDEX and NOT from the Working area.

 

**MOVING and RENAMING files**

 

Let\'s say our goal is to rename a file named menu.txt. In this case we know that renaming is similar to \*moving. So when we rename the file and then run the **\<git status\>** command\... we see that we have 2 files now\... ONE that\'s being added (our newly renamed one) and ANOTHER that\'s being deleted (our original file). Though this might look confusing within the context of the WORKING AREA and the INDEX\.... once we add BOTH changes to the Staging Area\.... and then run a **\<git status\>** command, then we see that git recognizes that we are dealing with a renamed file.

 

There is a nicer way of handling this kind of task though\...

**\<git mv meny.md meny.txt\>** This command should be pretty straight forward\... It moves the files in the working area AND updates the index\... it just does it in a single shot.

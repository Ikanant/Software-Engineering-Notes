More Tools

Sunday, August 4, 2019

4:26 PM

**THE STASH AREA**

In the first few pages of these notes I mentioned how there are 4 AREAS within our GIT repositories that we need to track\... the one we ignored until now is the **STASH**

The reason why we put it aside is because all of the commands we have gone over so far have certain effect across the Working/Index/Repository areas, but none play a role on anything related to the Stash.

There is only one command that affects the stash:

**\<git stash\>**

Now, image a case in which we have all of our work put together in our Working Area and even in the Index

![Stash Working Area menu. txt e guacamole. txt Index menu . txt e guacamole. txt Repository menu . txt ](003_More_Tools_000.png)

But then I realize that I need to work on something else? \-- specially if that something else needs to happen on the same branch\... do a loose everything then? No\... we can use the stash.

**\<git stash save\> or \<git stash\>** And everything that\'s in the Working Area and the Index will be saved\... ONE nice flag to have is --include-untracked

**\<git stash --include-untracked\>**

By default git will ignore untracked files so, passing in this flag will make sure you don\'t leave anything behind.

So what is actually happening? - Simple. GIT is copying ALL of the data from the Working Area and Index that is not in the current commit in the Repository into the Stash and THEN it also CHECKS OUT the current commit\...

![Stash menu. txt guacamole. txt Working Area o menu. txt Index o menu . txt Repository o menu . txt ](003_More_Tools_001.png)

In order to see what is currently on the Stash we can simply:

**\<git stash list\>**

We can store as many elements as we want in the Stash.. And each element there gets labeled with information about the latest commit\... and it also get\'s a serial ID 0-\...

In order to GET things that have been stashed\...we use

**\<git stash apply\>**

\^\^\^ if we don\'t specify the name of the stash element it will grab the most recent element by default\...

Once we are done with the Stash content, we would clear it

**\<git stash clear\>**

Note that when applying a Stash it DOES NOT delete it.

**Solving Conflicts (Merge)**

![cookbook\> cat recipes/guacamole. txt Ingredients: Avocados Lime juice Serrano chiles Ci Ian tro Salt Black pepper cookbook\> git branch tomato cookbook\> git checkout tomato Swi tched to branch \'tomato\' cookbook\> vim recipes/guacamole. txt cookbook\> git add recipes/guacarnole . txt cookbook\> git commit -m \"Add tomato to guacamole \"1 ](003_More_Tools_002.png)

Notice how in the scenario above I created a brand new branch, checked it out\... added an item to my list in the .txt file\... Let\'s assume now that the guacamole.txt file ALSO changed on the master branch\... what would happen?

MERGE CONFLICT

Now, let\'s say that we want to merge our tomato change into our master branch\... how do we do this?

**\<git merge tomato\>**

\^\^\^ We merge here by \*being in the master branch and pulling data from the tomato branch.

![cookbook\> git merge tomato Auto-merging recipes/guacamole. txt CONFLICT (content): Merge conflict in recipes/guacamole. txt Automatic merge failed; fix conflicts and then commit the result. cookbook\> git Status On branch master Your branch is ahead of \'origin/master\' by 5 commits. (use \"git push\" to publish your local comnli ts) You have unmerged paths. (fix conflicts and run \"git comit\") (use \"git merge ---abort\" to abort the merge) (use \"git add \" to mark resolution) Unmerged paths: both modified: recipes/guacamole . txt no changes added to commit (use \"git add\" and/or \"git commit -a\") ](003_More_Tools_003.png)

Git is pretty good at solving these problems\... but in this case we are looking a the case where both branches have changes right on the same line. GIT cannot decide which change comes first\... so it CHANGES the file in the WORKING AREA to give us enough information to solve the conflict ourselves\...

\^\^\^ This is the FIRST way that a merging conflict impacts the 4 areas\... before looking into the file in more detail\.... one question:

How does GIT know we are in the middle of a merge (that has a conflict) when running the

**\<git status\>** command?

Well, it knows because the merge commands creates files in the .git directory that signal that there is a merge operation going on\... This data will also save the information about WHAT is being merge too..

![3 4 5 6 12 gredients: Avocados Line juice Serrano chi les Ci lantro salt HEAD Onion Tomato tomato ](003_More_Tools_004.png)

Now when analyzing the file that is having the conflict one thing to note is that:

-   HEAD: Is the current COMMIT

-   Tomato: is the Tomato branch

Now we can manually fix this issue\... (there are plenty of tools out there to do that in a nicer user interface).

Now that we fixed things\.... we need to tell GIT. In fact running

**\<git status\>**

will still see a conflict\... essentially we are in charge of using the INDEX (Staging Area) to tell GIT that I solved the problem\...

**\<git add recipes/guacamole.txt\>**

\^\^\^ This is the command we need now. In this case our add command is just a bit more specific. It means, this file is ready to be committed because I SOLVED the merging problem.

**\<git commit\>**

And we are DONE\.... no need to specify msg since that was already coming from the merge task.

**Working with PATHS**

Working with COMMITS can sometimes be rough\... if we sync back to what I mentioned earlier about COMMITS being a snapshot of your entire project, we can think that SOMETIMES we just need to work with something smaller that our entire project (single file or directory).

![Working Area menu . txt README . txt Index menu . txt README . txt Repository o menu. txt O README. txt ](003_More_Tools_005.png)

Take the above example\... let\'s say that I have these 2 files edited and ready to be commited to my Repository\... but suddenly I am not so sure about one of them\... maybe I want to commit just one out\... what do I do?

As before, we could always do a **\<git reset HEAD\>** but to do it even better we can just say:

**\<git reset HEAD menu.txt\>**

But let\'s go one stage further then\... let\'s say that we also wanted menu.txt to be cleaned in our Working area as well\... could we do:

**\<git reset --hard HEAD menu.txt\>\
**NO

GIT doesn\'t allow for this\... the most common way to revert a single file or directory in the Working Area without touching other files is to use CHECKOUT

**\<git checkout HEAD meny.txt\>**

Woah \^\^ cool. So normally CHECKOUT moves the HEAD reference in the repository (usually to a branch) and then it copies ALL the files from the repo to the Working Area and the Index\... in this case\... CHECKOUT is NOT going to move HEAD\... Checkout is just going to COPY stuff from the CURRENT COMMIT in the repository for the ONE file we specified\... KEEP IN MIND: This is one of the most destructive operations you can do in GIT. We didn\'t even get a warning\... so, WATCH OUT!

Exploring the Past

Monday, August 5, 2019

7:37 PM

 

When exploring the history of our repository, we will undoubtfully be diving into COMMITS.

 

Starting out simple, if we have a certain branch checked out in our working area we can simply do something like

 

**\<git log\>** This is not my personal way to figure things out in GIT since every commit gets placed in one long list that is very hard to parse through\... we can make this a bit better:

 

-   \-- graph: Gives us a graph structure where we can see how the commits branch and merge

-   \-- decorate: Shows the positional references like branches HEAD

-   \-- oneline: This will make it so each commit only takes one line

>  

**\<git log --graph --decorate \--oneline\>**

 

![cookbook\> git log \--graph \--decorate \--oneline 716ød61 (HEAD -\> nogood , origin/nogood) Remove sugar \* a87f2cc Add more apples \* ecbebe6 (origin/lisa, lisa) Merge branch \' lisa\' \* ee7ffe9 Add Lisa\'s version of the pie I e268621 Add recipe l/ \* 572efdf Add cake \* 11779f4 First commit! cookbook\> I ](004_Exploring_the_Past_000.png)

 

 

Let\'s now say we want to see information about the current commit\... what information were introduced by this commit.. The date which it was introduced and so on\...

 

**\<git show HASH\>** for example **\<git show 7160d61\>**

 

However, using HASHES is not always the best way to retrieve history\... another way to tackle this is by giving the NAME OF THE REFERENCE that is pointing to the COMMIT\... the branch name or HEAD would work:

 

**\<git show HEAD\>**

 

What if we want to reference an older commit\... since there is no reference pointing to it, the only way to deal with it is to use the HASH\... no?

 

Well we can always use \^

 

SO, if we do something along the lines of **\<git show HEAD\^\^\>** we would be getting the info from the 2 commits parents of HEAD\...

 

![HEAD nogood 7160d61 a87f2cc 6 e268621 007ffe9 5720fdf 11779f4 ](004_Exploring_the_Past_001.png)

 

 

**We can ALSO use \~**

 

**\<git show HEAD\~2\>**

 

This type of SHOW commands work well, except as soon as we have multiple parents to one COMMIT.

 

**\<git show HEAD\~2\^2\>** This will show the info from the 007 commit above. Start from HEAD, the Go back 2 commits\... then pick the 2^nd^ parent.

 

There are cooler ways like:

 

**\<git show HEAD@{\"1 month ago\"}\>**

 

Now let\'s say we want to check the specific person who committed a line in a file\... similar to SVN we can do something like:

 

**\<git blame SageworksAnalystRoot/index.aspx\>**

 

![cookbook\> git blame recipes/apple_pie. txt 05-13 2e15-1ø-03 •4e:11 2e15-1ø-03 18:40. 2e15-1ø-ø3 2e15-1ø-ø3 2e15-1ø-03 2e15-1ø-e4 1779f4 e2686215 e2686215 e2686215 e2686215 ee7ffe99 a87f2ccb (Paolo (Paolo (Paolo (Paolo (Paolo (Paolo (Paolo \"Nusco\" Perrotta 2e15 Perrotta per rotta Perrotta Perrotta perrotta Perrotta 18. 18. 18 .11 402eo .e2eø \*02eo 402ea .e2eø -te2eo .e2eø I) 2) 3) 4) 5) 6) 7) Apple Pie pre-made pastry 1/2 cup butter 3 tablespoons flour 1 tbsp cinnamon 2e Granny Smith apples ](004_Exploring_the_Past_002.png)

 

We could also check out the difference between two commits\... we can use the DIFF command (as we did before\.... but this time we will be comparing 2 COMMITS)

 

**\<git diff HEAD HEAD\~2\>**

 

AND of course we could also compare branches with our repos:

 

**\<git diff feature/AD-1234 master\>**

 

Keep in mind that GIT LOG is literally one of the most complex and aweosme commands at our disposal when working with GIT\....

 

<https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History>

 

Check out the documentation since it\'s pretty impossible to remember everything\...

 

**\<git log \--grep Workflow \--oneline\>**

This will for example retrieve every single commit that has the word \'workflow\' in it.

 

**\<git log --GWorkflow \--patch\>**

This will retrieve all the commits that added the word Workflow on ANY file. Patch will allow us to see what lines example were impacted with these changes

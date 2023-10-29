Git Reset

Sunday, August 4, 2019

2:13 PM

 

RESET is one of those commands that can be scary to most people. I had issues with it at first\... One thing we always learn first about reset is that\'s a potentially destructible operation\... so when working on big projects it is scary to use it confidently.

 

Why is RESET confusing?

1.  To understand **\<reset\>** we need to understand the three main AREAS and GIT branches.

2.  It does different things in different contexts

    a.  Googling how to reset things in git often leads to lots of results on google with different variations that have different outcomes depending on our task

>  
>
>  

What are some commands that we know that move branches?

-   **Commit**

    -   It creates a new commit, and it moves the current branch to this commit

-   **Merge**

    -   (Creates a Commit in most cases)... it also moves the current branch to part of the new commit

-   **Rebase**

    -   It creates new commits by copying existing commits and it moves the current branch to the point where our new commit is created

-   **Pull**

    -   Gets new commits from the REMOTE and updates the local branches

>  
>
>  

All the commands above move branches; HOWEVER, none of them are specialized operations to move such branches. These commands move branches as a side effect\...

 

The one command we have in GIT to explicitly move a branch is **\<reset\>**

 

If we are ONLY looking at the repository, RESET pretty much moves a branch to point at a specific commit..

 

 

![](002_Git_Reset_000.png){width="2.875in" height="1.6583333333333334in"}

 

![master HEAD ](002_Git_Reset_001.png){width="2.933333333333333in" height="2.1166666666666667in"}

 

Though one thing to note here is that we are NOT moving the current HEAD, we just move a branch and HEAD just so happens to tag along.

 

The weird thing that I find about RESET is not the repository step, instead I focus on the second thing that happens to the Working Area and the INDEX.

 

**\--hard:** The RESET will copy data from the new current commit to both the Index and the Working Area:

![Working Area Index Repository \--hard ](002_Git_Reset_002.png){width="5.0in" height="2.066666666666667in"}

 

**\--mixed:** This will move data from the Repository to the Index (Staging area)... this is the **DEFAULT** option if we don\'t specify any flag

 

![](002_Git_Reset_003.png){width="5.0in" height="2.066666666666667in"}

**\--soft:** It just updates the Repository side and does NOT touch anything in the WorkingArea/Index\... just move the branch and skip everything else

 

**RESET:** Moves the current branch and optionally copies data from the Repository to the other areas

 

 

**EXAMPLE**

 

**\<git log\>**

This will show the current commit and the previous commit as a parent\...

 

![Working Area menu. txt recipes Index menu. txt recipes HEAD fbe535 Repository menu. txt recipes commit fbe53568fadc55b5f2f22617c57d320878aØ8767 Author: Paolo \"Nusco\" Perrotta Thu Jul 28 2016 +0200 Date: Well, I changed my mind about that renaming commit lcb2137eb1bf282ff87aae82c2fcc3405aaøae91 Author: Paolo \"Nusco\" Perrotta \<paolo.nusco.perrotta@gmail.com\> Thu Jul 28 2016 +0200 Date: Use Markdown for the menu commit 8Øf2a48777ffe5ab3cOccd2d3eba2c06ce4a7f2e Author: Paolo \"Nusco\" Perrotta \<paolo. wed Jul 27 13:11:37 2016 +0200 Date: cookbook\> ](002_Git_Reset_004.png){width="5.0in" height="3.066666666666667in"}

 

Let\'s say that we added two more commits on the branch above\.... and later we regret those commits\... well, if we wanted to go back to the fbe commit above\... we would do:

 

**\<git reset --hard fbe5356\>**

Though we need to keep in mind that the first thing that happens is that git moves the branch back to that previous commit\... and HEAD follows along. Since we are doing a hard reset, GIT also takes everything from the the repository and spreads it across the Working Area and the Index area accordingly

 

![Working Area o menu. txt o recipes Index O menu. txt O recipes Repository Obe2a5 ](002_Git_Reset_005.png){width="5.0in" height="1.3416666666666666in"}

 

 

Now keep in mind that because we now have some commits with NO branches pointed to them\... these will be garbage collected at some point.

 

**EXAMPLE 2**

 

Let\'s say that we have a file edit pushed to the INDEX AREA\.... and that later on we realize that we actually do not want to have that there YET\... earlier we saw how doing something like **\<git rm \--cash\>** was an option\.... BUT if we look at things carefully when we run a **status** check\... we see that GIT recommends using RESET.

 

**\<git reset HEAD \<file\> ...\"**

 

This means that we are moving the current branch to the commit pointed at by HEAD\... BUT the current branch is already pointed to that commit\... so in this case the RESET will not move the HEAD at all because there is no where to move it (We are essentially skipping the first step of this task all together)... What\'s the second step??? \-- remember that GIT moves data by default from the REPO to the STAGING area\... (\--mixed) ... so this will move data from the current commit to the index but NOT the working area

 

**EXAMPLE 3**

 

Let\'s say we do not want anything else to be committed and we want to scratch EVERYTHING that has been changed across our AREAS\.... we would do a

 

**\<git reset --hard HEAD\>**

This will NOT move the branch because it\'s still a HEAD reset\.... BUT it copies data from the REPO to the INDEX and WORKING AREA\...

 

This is a common/useful command BUT it is one that needs to be used with care\... because this can be destructive.

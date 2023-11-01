Fixing Mistakes

Monday, August 5, 2019

9:02 PM

In the previous section I talked about how to SEE the project history in our repository\... now let\'s go over how to EDIT that history\...

Quick note on REBASING: We should never REBASE shared commits. Once we push a commit to a shared repo, we should avoid the rebase command\... this is because the REBASE is a command that changes history. The new COMMITS might look the same as the old ones\... but they are actually NEW commits in the Database\... As a result other people can get real confused about commits that they also had in their repository.

**The Golden Rule:** Never change shared history! (with any command that changes history)

**Changing The Latest Commit**

We have all been there, where we changed a bunch a files in our local environment, maybe even deleted one or two, and we go ahead and commit the change to the repo without realizing we have not YET saved the .csproj file\.... that sucks! Now our branch has a commit that certainly would yield a broken build (REMEMBER THIS SHOULD NOT BE HAPPENING ON SHARED BRANCHES LIKE MASTER).... Now, we can always SAVE the .csproj file again\... stage it and commit everything\... what\'s wrong with that? Technically nothing\.... but I don\'t want the people of my team to know that I made such a rookie mistake\....well, that\'s where the AMEND argument fixes our problem\....

**\<git commit \--amend\>** Will take the changes that are in the staging area and they will be applied to the last commit in the REPO\.... even giving us the option to change the commit msg.

What actually happens behind the scenes here is that GIT will create a BRAND new commit with ALL of the changes together, and then it will move the MASTER / HEAD titles to that commit, leaving the other one ORPHAN\... the old branch will be garbage collected at some point.

![master 5de2465 5127436 a8e182e ](005_Fixing_Mistakes_000.png)

**Regular REBASING (copied from the web by request)**

The commits that were previously saved into the temporary area are then reapplied to the current branch, one by one, in order. Note that any commits in HEAD which introduce the same textual changes as a commit in HEAD..\<upstream\> are omitted (i.e., a patch already accepted upstream with a different commit message or timestamp will be skipped).

It is possible that a merge failure will prevent this process from being completely automatic. You will have to resolve any such merge failure and run git rebase \--continue. Another option is to bypass the commit that caused the merge failure with git rebase \--skip. To check out the original \<branch\> and remove the .git/rebase-apply working files, use the command git rebase \--abort instead.

Assume the following history exists and the current branch is \"topic\":

A\-\--B\-\--C topic\
/\
D\-\--E\-\--F\-\--G master

From this point, the result of either of the following commands:

**\<git rebase master\>**

**\<git rebase master topic\>**

A\'\--B\'\--C\' topic

/

D\-\--E\-\--F\-\--G master

REBASING can get complicated so I recommend checking out before continuing:

<https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase>

**INTERACTIVE REBASING**

This is where an Interactive Rebase comes into place\.... Interactive REBASES is literally ONE of the most MOST POWER TOOLS EVER when it comes to GIT\.... looks something like (GIF):

![WIP (Work In Progress) ](005_Fixing_Mistakes_001.png)

Here is what we need to keep in mind\... if we do an INTERACTIVE REBASE\... the REBASE is no longer a regular rebase like the one we are used too\... instead this will become one of the MOST powerful tools in GIT to change history.

![cookbook\> \* 2c74ea2 \* 5127436 \* a8e182e git log \--oneline \--decorate ---graph (HEAD master) Add missing chicken tikka masala placeholde Add Caesar Salad to menu Make README all uppercase \* f22døad Merge branch \' tomato\' I \* øc55d2f (tomato) Add tomato to guacamole \* 1 7fd9bb2 Add onion to guacamole 1 fc6aef \* \* fbe5356 lcb2137 \* \* 80f2a48 \* 704182f \* 5d4a817 ca760f8 \* \* bf36d97 fced3af \* Add guacamole Well, I changed my mind about that renaming Use Markdown for the menu Add Tikka Masala to menu (origin/master, origin/HEAD) Add lemon juice to the apple pi (origin/spaghetti, spaghetti) Add carbonara ingredients Add spaghetti alla carbonara Tweak apple pie some more Tweak apple pie ecbebe6 (origin/lisa, lisa) Merge branch \'lisa\' I \* 07ffe9 Add Lisa\'s version of the pie \* I e268621 Add recipe \* 5720fdf Add cake \* 11779f4 cookbook\> git rebase -i origin/masterl ](005_Fixing_Mistakes_002.png)

What we are saying above is that we are going to REBASE (change the history of our branch fromm the ORIGIN/MASTER, we could also use a HASH here\... to the latest COMMIT in our branch\...

**\<git rebease \--interactive REFERENCE_COMMIT\>**

or

**\<git rebase -i REFERENCE_COMMIT\>**

Now we enter the text editor to rewrite a computer program. The program will go line by line executing each line and performing whaterver task we want it to do:

![2 3 4 5 6 7 8 pick pick pick pick pick pick pick pick sef2a48 lcb21 37 fbe5356 1 fc6aef 7fd9bb2 Oc55d2f a8e182e 5127436 2c74ea2 Use Markdown for the menu Well, I changed my mind about that renaming Add guacamole Add onion to guacamole Add tomato to guacamole Make README all uppercase Add Caesar Salad to menu Add missing chicken tikka masala placeholder ](005_Fixing_Mistakes_003.png)

WHICH THEN WE CHANGE TO:

![2 3 4 5 6 7 8 9 pick 80f2a48 Add Tikka Masala to menu squash 2c74ea2 Add missing chicken tikka masala placeholder pick lcb2137 Use Markdown for the menu reword fbe5356 Well, I changed my mind about that renaming pick 1 fc6aef Add guacamole squash 7fd9bb2 Add onion to guacamole squash Oc55d2f Add tomato to guacamole pick a8e182e Make README all uppercase pick 5127436 Add Caesar Salad to menu ](005_Fixing_Mistakes_004.png)

Whenever there is an item that needs a decision from us (the developers) that\'s when GIT pasues the rebase and shows you another text editor to make changes\... Let\'s say we are squashing two commits\... What this means is that GIT is going to get the changes from those commits and make them into one\... since each of those commit had a commit msg\.... GIT is going to ask us to update that\...

![2 3 4 5 6 8 This is a combination of 2 commits. \# The first commit\'s message is: Add Tikka Masala to menu \# This is the 2nd commit message: Add missing chicken tikka masala placeholder ](005_Fixing_Mistakes_005.png)

The one thing to keep in mind with this process is that, let\'s consider the case in which we have a merging conflict (product of one of the squash steps) ... GIT is going to pause the task and allow you to fix the conflict like a regular rebase\..... once you go to the affected files and are ready to continue, you write\...

**\<git add CONFLICTED_FILE\>**

**\<git rebase \--continue\>**

**The Reflog**

![master HEAD ](005_Fixing_Mistakes_006.png)

So, looking at  the interactinve rebase we did above, what we essentially do when rewriting history like this is to create another branch, move our labels around and let the older branch get deleted later on\....but, what if I changed my mind?

ANY TIME that we do anything in GIT it gets saved in the REFLOG

**\<git reflog HEAD\>**

This command will show me EVERYTHING that has happened in my GIT command history and it will even include the HASH code of each step\...

![1762c e 5d4a81 7 1762cfe -i -i dec24ed -i -i 772089c -i 8e579e1 c89f9fd -i 3Ø3e282 -i -i 319e02e dØa6bfe 8Øf2a48 2c74ea2 51 27436 a8e182e 7160d61 a8e182e f22dØad 7fd9bb2 I fc6aef 1 fc6aef I fc6aef fbe5356 beb74ØØ fbe5356 checkout : checkout : 1762cfe 1Øfd574 5de2465 Oc55d2f rebase rebase rebase rebase rebase rebase rebase rebase rebase rebase rebase commi t : commi t commi t : moving from spaghetti to master moving from master to spaghetti (finish): returning to refs/heads/master (pick): Add Caesar Salad to menu (pick): Make README all uppercase (continue): Add guacamole (squash): \# This is a combination of 2 commits. (pick): Add guacamole (reword): Fix bad renaming (reword): Well, I changed my mind about that renaming -i (pick): Use Markdown for the menu -i (squash): Add Tikka Masala to menu -i (start): checkout origin/master Add missing chicken tikka masala placeholder (amend): Add Caesar Salad to menu Added Caesar Salad to menu checkout: moving from nogood to master checkout: moving from master to nogood commit: Make README all uppercase commit (merge): Merge branch \'tomato\' commit: Add onion to guacamole checkout: moving from tomato to master commit: Add tomato to guacamole checkout: moving from master to tomato commi t : reset: commi t : commi t : Add guacamole moving to fbe53568 Add placeholder recipe for squids Well, I changed my mind about that renaming ](005_Fixing_Mistakes_007.png)

By looking at this list we can go ahead and take a look at what changed when:

**\<git show HEAD@{15}\>**

The information in the reflog is strictly local information\.... and one way we can keep the garbage collector from removing some important data out of is is by pointing a branch to one of these commits.

**Reverting COMMITS**

So how about the case in which I am working on a feature branch and after 15 commits I realized I never needed the very first one? - I am too lazy to create yet another commit removing it and I take upon myself to CHANGE HISTORY\.... well, one way to do it is by utilizing the interactive rebase tool we saw earlier\.... but that is no fun\.... that would literally create a brand new set of 14 commits that will then need to be pointed and wait for the garbage collector to clean the old one\.... I DO NO WANT THAT.

Well, the right answer to this dilemma is

**\<git revert HASH\>**

This is essentially the same thing as if we were to fix the code issue ourselves and committed the fix onto the end of the history\... ONLY difference is that GIT will take care of things for us\... it will essentially edit the files in our working area with the opposite to what the commit we specified had!

**\<git revert 5720fdf\>**

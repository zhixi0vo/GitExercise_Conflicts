MERGED EX1

# GitExercise_Conflicts

<<<<<<< HEAD

## Purpose
To teach you to deal with git merge conflicts in 
- Jupyter Notebooks
- on Datahub using graphical notebook based tools

The instructions here are specific to the COGS 108 Datahub setup. 

Note that this is different than your previous exercises... they were on GitHub (not on Datahub) and there were no graphical diff tools in use



## Problem overview

This repo contains two branches: main and ex1. There is a single line text conflict in one cell between the two branches, as well as other line differences that do not conflict.

Below is a graph of the commit situation in the repo right now... each * indicates a commit and the lines show the evolution of the repo over time
=======
This exercise assumes you are using the COGS 108 Datahub setup.  But you can do everything here using your own computer if you set it up with the same tools (which is recent Jupyterlab with the git extension built on nbdime). If you are using git command line or VSCode, or something else entirely then you can still do this exercise, but the step by step insructions will need to be adapted to your tools.  There is always more than one way to get something done, just learn and use the tool that you prefer!

This repo contains two branches: main and ex1. There is a single line text conflict in one cell between the two branches. The goal of this exercise is 
two-fold; to learn how to stage and commit changes to a branch and then to learn how to merge the changes from one branch to another.

Below is a graph of the commit situation in the repo right now... the commits on each branch have produced a single line conflict you need to deal with before merging
>>>>>>> ex1

```
----*----*[main]
     \
      \----*[ex1]
```

We will do two seperate git operations 
- [Part 1] add a new change to branch main, thus introducing a second difference with ex1 branch
- [Part 2] then we will merge the changes from branch ex1 into main

Thus after Part 1 the new graph will look like

```
----*----*----*[main]
     \
      \----*[ex1]
```

And after Part 2 the new graph will look like

```
----*----*----*----*[main]
     \             /
      \----*------/
```

<<<<<<< HEAD
## Setup this stuff first
1. Fork this repo by pressing the Fork button at the top of this webpage
     - When forking **UNCHECK** the default option to "Copy the main branch only". You want all the branches!
     -  Forking this repo made a copy of this repo on YOUR GitHub.  You have direct write access to the forked copy, but not the original repo
1. Let's get a local copy of your forked repo...
     - login to Datahub
     - if you have not already created SSH keys for datahub, do so now and place them on your GitHub account per https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account  <br> **NOTE:** these keys are different than the ones you made on your laptop. Each computer you use with GitHub needs its own keys!
     - Open a terminal window on Datahub.
     - Type: `cd ~/private` which will put you inside a subdirectory of your datahub file system.
     - Type: `git clone git@github.com:your_username/GitExercise_Conflicts.git` <br> but replace  `your_username` with your actual GitHub username
     - Your new local copy of the repository will appear in the file browser inside the folder `~/private/GitExercise_Conflicts` Double click around the file browser until you find the folder and open it

## Part I - Make a local change on main
1.  Open `Project.ipynb`
     -  Just for fun (you don't have to do this substep, but its a good teaching point)
          -  run both cells of the notebook to see the plot
          -  Unfortunately running the notebook changes the metadata stored inside it.  The counter for how many times a cell was run, the binary data from the plot.  This is stuff we do NOT want to version control... its not important and it clogs up the system because notebook metadata for plots can be very big.
          -  Save the notebook, open a terminal window in this directory and type `git diff`, now you will see the insane line differences generated just by running the notebook
          -  Before we do any git operations it is a best practice to click on the pulldown menu item `Edit -> Clear Outputs of All Cells`.  Do this now, and press save so we don't have to put this BS into the git history
1. Lets add a change we do want:
     - the last line of the notebook currently says `ax.grid()` which (although it works) is bad Python form...
     - change it to the more readable and more Pythonic `ax.grid('on')` 
     - save the file when you are done!
1. Add / commit the changes using the GUI (git extension for Jupyterlab)
     - Yes you could do all this in the terminal window, but I'm showing you the GUI way here.  If you're a command line hero, feel free to do this task there :)
     - On the far left you will see a vertical stack of icons in a grey panel.  Click on the one that's a diamond with some lines inside it, that's the git panel.
     -  At the bottom of the git panel you can see there are three categories of files that could be the subject of git operations <br>
         "Untracked" for new files you create that are not yet in the repo  <br>
         "Changed" for files already in the repo, but you changed something  <br>
         "Staged" which tracks all the changes you've asked to be grouped together into a commit  <br>
     -  Look at the "Changed" section, `Project.ipynb` is there... hover your mouse over it.  You will see icons for opening the file, for making a diff summary of the changes, for discarding the changes, and one for staging the changes for a commit (a + symbol).
     -  Stage the changes!
     -  Now that `Project.ipynb` is in the "Staged" category you can scroll down to the bottom of the git panel and commit the changes.  Add a summary (<50 characters), e.g.  "improved code readability".  There is also a space for longer description if necessary.  Press the "Commit" button, and you're done with Part I!

## Part II - Merge ex1 into main
1. Get a local copy of the ex1 branch using the GUI. <br> When you cloned the repository you only got a copy of the default branch "main"... there were other branches but they are still only on the remote repo up on GitHub.  Remote branches are marked with the keyword "origin". So "main" is a local branch, "origin/main" is the main branch on GitHub.
     - On the git panel there's a place at the top where it says "Current Branch: main"; click on that menu item to see a list of all the branches available.
     - Click on "origin/ex1", this makes a local copy called "ex1"  and sets it up to track the remote branch "origin/ex1".
     - Now that we have local copies of both main and ex1 we can merge the branches
1. Merge ex1 into main
     -  OK here's the task: we want to merge the change in branch ex1 (a change of title on the graph) into main, keeping the ex1 title erasing the old title on main.  But we want to keep our `ax.grid('on')` change which is only on main and not ex1. 
     -  Here's how to do it... click on "main" to make sure we are currently on the main branch.  We want to be on the branch that is the destination of the merge.
     -  Hover over the local "ex1" branch and a button icon that looks like 3 dots with connecting lines will appear.. when you hover over the button it says "merge this branch into the current one"... go ahead and click it!
     -  You will get an error message "Failed to merge ex1 into main".  And now there is a new category "Conflicted" just above "Staged"!  Our file `Project.ipynb` is in that heading as expected!  Hover over the file, and click on the icon to "diff this file" that appears.
     -  You will now see the diff panel... where there are conflicts you have from left to right three possiblities: <br>
         "Current" (what was in main before the merge) <br>
         "Common Ancestor" (what the file looked like when ex1 split off from main) <br>
         "Incoming" (what was in ex1 before the merge) <br>
         Underneath the triple column you will see a panel where you can manually change the conflict zone to make the outcome what you want.  Whatever you put in this lower panel is what the outcome of the merge will be!
     - Make the outcome of the merge to be the ex1 title and the main ax.grid('on') command!  Save it by clicking the button on the top right that says "Mark as resolved". You will see that `Project.ipynb` moved from "Conflicted" to "Staged"
     - Go look at the notebook and make sure it is what you wanted it to be.
     - It is also useful at this stage to Restart-kernel-and-run-all to ensure that the Frankenstein's monster of code from both branches is actually functional as a combo. A lot of difficult to solve runtime errors come from failing to test the integrated code after the merge! 
     - When you're finished with the run-all then `Edit -> Clear Outputs of All Cells` before saving to get rid of the useless metadata changes that we do not wish to add to git.  Save the file, add commit the file if git tells you this is an unstaged change.
   
## After Part I / II DO THIS or LOSE POINTS 
All the changes you've made so far only exist in the local copy on Datahub. We need to push the changes from the local copy to your forked copy. 

On the top left of the git panel are a set of cloud icons, one with the arrow pointed down (that's pull) and one with the arrow pointed up (that's push).  In general: If there's a red dot on one of the clouds you need to do that action.  

1. Push your exercise. Now you're done! The changes you've made have appeared on GitHub and are visible to other people including our auto-grading scripts.
     - Failing to push will mean you don't get the autograder's points on A1
     - If the push fails its probably because you
          - either cloned the COGS108 repo instead of the fork that lives in your GitHub.  
          - or you used http access to clone instead of ssh access.
          - whichever one it is, to fix it you will need to change the origin so it points at the fork using ssh not http; I'd suggest coming to a TA for help with this.  
  
## Congrats!! 
You've dealt with a simple version of the notebook conflict problem. This workflow will happen in your projects all the time, when person A and person B need to merge their seperate parts of the project together into the final project. 
=======
To work on this exercise:
- Fork this repo by pressing the Fork button at the top of this webpage.  When you fork it MAKE SURE you **UNCHECK** the default option to "Copy the main branch only". You want all the branches!
-  Forking this repo made a copy of this repo on YOUR GitHub. You own this fork, you can change it however you like.
- The original repo was at `https://github.com/COGS108/GitExercise_Conflicts.git`, your forked copy will be located at `https://github.com/your_username/GitExercise_Conflicts.git` where you must replace `your_username` with your actual GitHub username.
- Note that the fork is a remote copy on GitHub... you will have to go to Datahub, login, and get a local copy of the fork (NOT the original) repo there.
- Let's get that local copy... login to Datahub.
- Use the Datahub file browser to make sure you are in a directory you are allowed to write new files to, e.g. the `private` directory inside your home directory.  Double click on the file browser to set your current working location to whatever is best for how you want to organize files.  Wherever you are in the file browser is where the new git repo will be created.
-  On the far left you will see a vertical stack of icons in a grey panel.  Click on the one that's a diamond with some lines inside it, that's the git panel.
-  Click the button "Clone a Repository" and set remote URL to `https://github.com/your_username/GitExercise_Conflicts.git` where you must replace `your_username` with your actual GitHub username. Click the button that says `Clone`
- Your new local copy of the repository will appear in the file browser... double click on the new folder `GitExercise_Conflicts` to go inside and view the files!

Part I - Make a local change on main
-  Open `Project.ipynb`
-  Just for fun, run both cells of the notebook to see the plot
-  Unfortunately running the notebook changes the metadata stored inside it.  The counter for how many times a cell was run, the binary data from the plot.  This is stuff we do NOT want to version control... its not important and it clogs up the system because notebook metadata for plots can be very big. Before we do any git operations it is a best practice to click on the pulldown menu item `Edit -> Clear Outputs of All Cells`
- Lets add a change: the last line of the notebook currently says `ax.grid()` which is bad Python form... yeah it works to turn on the grid lines of the plot implicitly, but it would be much more human readable if we used the more Pythonic `ax.grid('on')`.  Please make that change and don't forget to save the file when you are done!
-  On the far left you will see a vertical stack of icons in a grey panel.  Click on the one that's a diamond with some lines inside it, that's the git panel.
-  At the bottom of the git panel you can see there are three categories of files that could be the subject of git operations <br>
    "Untracked" for new files you create that are not yet in the repo  <br>
    "Changed" for files already in the repo, but you changed something  <br>
    "Staged" which tracks all the changes you've asked to be grouped together into a commit  <br>
-  Look at the "Changed" section, `Project.ipynb` is there... hover your mouse over it.  You will see icons for opening the file, for making a diff summary of the changes, for discarding the changes, and one for staging the changes for a commit (a + symbol).  Stage the changes!
-  Now that `Project.ipynb` is in the "Staged" category you can scroll down to the bottom of the git panel and commit the changes.  Add a summary (<50 characters), something like "improved code readability".  There is also a space for longer description if necessary.  Press the "Commit" button, and you're done with Part I!

Part II - Merge ex1 into main
-  On the git panel there's a place at the top where it says "Current Branch: main"; click on that menu item to see a list of all the branches available. When you cloned the repository you only got a copy of the default branch (called "main")... there were other branches but they are still only on the remote repo up on GitHub.  Remote branches are marked with the keyword "origin". So "main" is a local branch, "origin/main" is the main branch on GitHub and likewise "origin/ex1" is on Github.  Click on that last branch... 
-  Previously you had only "origin/ex1" and not "ex1", but now you do!  By clicking on "origin/ex1" git made a local branch "ex1" and set it up to track the remote branch "origin/ex1".  Now that we have local copies of both main and ex1 we can merge the branches.  ex1 will be merged into main!
-  OK here's the task: we want to merge the change in branch ex1 (a change of title on the graph) into main, erasing the old title.  But we want to keep our explicit `ax.grid('on')` change which is only on main and not ex1. 
-  Here's how to do it... click on "main" to make sure we are currently on the main branch.  We want to be on the branch that is the destination of the merge.
-  Hover over the local "ex1" branch and a button icon that looks like 3 dots with connecting lines will appear.. when you hover over the button it says "merge this branch into the current one"... go ahead and click it!
-  You will get an error message "Failed to merge ex1 into main".  And now there is a new category "Conflicted" just above "Staged"!  Our file `Project.ipynb` is in that heading as expected!  Hover over the file, and click on the icon to "diff this file" that appears.
-  You will now see the diff panel... where there are conflicts you have from left to right three possiblities: <br>
    "Current" (what was in main before the merge) <br>
    "Common Ancestor" (what the file looked like when ex1 split off from main) <br>
    "Incoming" (what was in ex1 before the merge) <br>
    Underneath the triple column you will see a panel where you can manually change the conflict zone to make the outcome what you want.  Whatever you put in this lower panel is what the outcome of the merge will be!
- Make the outcome of the merge to be the ex1 title and the main ax.grid('on') command!  Save it by clicking the button on the top right that says "Mark as resolved". You will see that `Project.ipynb` moved from "Conflicted" to "Staged"
- Go look at the notebook and make sure it is what you wanted it to be.  It is also useful at this stage to run-all to ensure that the Frankenstein's monster of code from both branches is actually functional as a combo.  You will get a warning that you have made changes that are unsaved because every time a notebook runs it changes metadata stored inside it. Ignore that... if you press save again you will add a new set of changes that need to be staged and committed, but those changes are USELESS... its just increments to the run counter of the cells and the exact binary data of the plot generated.
- Let's commit the merge!  On the git panel give it a summary (something like "merged ex1 into main") and press the commit button.
   
Finally
- All the changes you've made so far only exist in the local copy on Datahub. We need to push the changes from the local copy to your forked copy.
- On the top left are a set of cloud icons, one with the arrow pointed down (that's pull) and one with the arrow pointed up (that's push).
- If there's a red dot on one of the clouds you need to do that action.  In this case you only need to push. Once you've pushed your exercise is done... the changes you've made have appeared on GitHub and are visible to other people including our auto-grading scripts.
- **IF YOU DON'T PUSH AT THE END OF THE EXERCISE YOU WILL LOSE POINTS ON THE AUTOGRADER** 
  
Congrats!! You've dealt with a simple version of the notebook conflict problem. This workflow will happen in your projects all the time, when person A and person B need to merge their seperate parts of the project together into the final project. 
>>>>>>> ex1

Another common project workflow is if there's a red dot on pull (down arrow) that means someone else made changes to the remote that you don't have.  Pull operations need to be done before push operations... so if someone changed the remote after your clone but before your push you will have to pull first, merge, and resolve any conflicts before you are allowed to push your changes to remote.  We didn't have to do that here, but its a very normal workflow for your projects.

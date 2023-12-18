# Git/GitHub

## Repository Standards

- Please refrain from pushing or merging directly to the main branch, except for tiny hot-fixes in exceptional situations (that have zero risk of breaking code).  Instead, create a short-lived branch, commit and push your changes, then issue a pull request to be reviewed then merged to `main`.
- Branch naming: [your_initials]/[feature_or_bug_name] (e.g. `nw/logging_bug_fix`)
- `main` is the only long-lived branch.  All other branches are short-lived and are intended to merge to `main` via pull-requests.
- all pull requests should be created with Daniel as a reviewer, and Daniel will add additional reviewers as necessary.  Feel free to list any additional reviewers you think could be helpful.
- the last reviewer to approve the request will merge the PR to `main` and delete the branch.

## Main Git / GitHub Workflows for Beginners

### Prerequisites / Background

- the following assumes you are using Windows and have TortoiseGit installed.  For Linux or Mac, if you are not yet familiar with the git command line, see [here](https://git-scm.com/docs).
- TortoiseGit has no dedicated user interface apart from the right-click menu in Windows Explorer.  To perform any of 
the git actions/verbs below, right-click the working copy folder in Windows Explorer and use the TortoiseGit submenu.
- Your working copy is simply a folder on your PC that holds a copy of the code, however it also has special tracking data that is used to signal git which revision and which branch you are pointed at at a given time.  At any given time, your working copy will be pointed at a given revision on your working copy, which is generally the head (latest revision) of a branch on your working copy.
- You can see which branch you are on at any point by right-clicking the working copy and looking at (but not clicking) the `Git Commit` command.  If you are on the `main` branch, it will say `Git Commit -> main`.
- Some devs commit often, and some commit less often.  As long as you are working on your own branch, it doesn't really matter how often you commit.  A commit doesn't have to be perfect code.  It is just a demarcation between steps in your dev process and gives you a specific revision of code that can always come back to, which is why many devs commit often to their own branches.
- All commits should be on your personal branch, not on the `main` branch.  This contributes to the goal that the `main` branch will at all times contain tested, reviewed code that can be deployed to a field device at any point (without worrying about half-baked or untested features that are in development).
- For each commit, it is often a good idea to also push that commit to the cloud immediately.  This ensures:
  - that no code is stored exclusively on your laptop (in case of data loss), and
  - that others can view your code if you need to ask for help
- Once your code is commited and pushed to GitHub, and after numerous commits, you have code you feel is ready to be included in the `main` branch, you will want to create a Pull Request (PR).  A PR is a formal request for the managers of the project to review and comment on your code.  It includes a description of what problem/bug/enhancement/feature you were trying to address in the commits that comprise your PR.
  - If rejected (a.k.a. `Changes Requested`), then you will need to do more commits to address the comments of the reviewer.
  - If approved, all the changes included in your short-lived branch is merged into the long-lived `main` branch, and your short-lived branch is usually deleted.  Subsequent work would be done by created another short-lived branch and repeating the cycle.

### Getting the code set up for the first time on your machine (`clone`)

- open a web browser and browse to the repo on GitHub (https://github.com/EMI-RnD/Rain_Logger)
- on the green `Code` button (top right), click the down arrow, and click the copy button just to the right of the repo git URL.  (`https://github.com/EMI-RnD/Rain_Logger.git` will be copied to your clipboard).
- on Windows Explorer, browse to a directory you would like to clone your new working copy into.
- in the white space (not on a file), right-click, and choose `Git Clone...`.  Set the URL to the value above (paste), and leave the Directory field as is if you are okay with that location.  Click OK.
- you should now have a 'working copy' of the code in your new folder, including a special .git directory in the root (which shouldn't be messed with).  This folder is a git working copy, which is a normal directory containing the repo files, but also has special git tracking info built in.  You can right-click this folder at any time and access the various git actions / verbs below.

### Pulling updates from the cloud (GitHub) to your working copy (`pull`)

- on Windows explorer, click on your working copy folder, and choose `Git Pull...`  (which may be under the `TortoiseGit` submenu)
- the default settings on this dialog (and others) can generally be left alone if they haven't been modified.  Click OK.
- Git will now:
  - pull the list of all branches on the cloud (a.k.a. GitHub) so your working copy knows about them
  - pull all revisions *on your current branch* from the cloud, and merge them into the same branch on your working copy

### Creating a new branch for new work

- ensure your working copy is 'clean' (e.g. has no changes).  If it does, either commit them or abandon them by doing a revert
- right-click on your working copy in Windows Explorer, and select `Git Switch/Checkout`.
- on the Branch drop down, ensure `main` is selected.  Click OK.  Your working copy is now pointed at the latest main branch revision that is in your local working copy.
- right-click on your working copy in Windows Explorer, and select `Git Pull`.  Click OK.  All revisions in the cloud's main branch have now been downloaded to your local working copy, and your main branch is now pointed at the latest code from the cloud.
- right-click on your working copy in Windows Explorer, and select `Create Branch`.  Enter the branch name (your initials and the feature/bug name, e.g. `nw/logging_bug_fix`).  Click OK.
- your working copy is now pointed at your new branch.  You can now start editing files on your working copy.

### Commiting (`commit`) and pushing (`push`) files to the cloud from my working copy

- after the files in your working copy are in a state that you want to commit (they don't have to be perfect - that's what a PR is for), right-click on your working copy in Windows Explorer, and select `Commit`.  The dialog will show you all the files that have been changed:
  - `Missing` files are files you removed from the folder, but haven't told git yet.  You can either:
    - right-click them and delete them (they will be marked for deletion from git's database on the next commit), or
    - right-click and revert them (bring them back to the version in the git database)
  - `Deleted` files are files you removed from the folder and told hit to delete.  These will be removed from the git database on the next commit (as long as the checkbox on the left remains checked).
  - `Modified` files are files that have been changed.  These will be updated in the git database on the next commit (as long as the checkbox on the left remains checked). **You can double click on the file to see a diff of what has changed in your version versus the previous rev.
  - `Unversioned` files are files that exist in the folder but git doesn't know anything about them.  You can either:
    - right-click them and add them (they are marked to be added to the git database on the next commit)
    - right-click and ignore them (the git repo will now ignore them, on your computer and everyone else's as well)
  - `Added` files are files that have recently been added to git, and will be added to the git database on the next commit (as long as the checkbox on the left remains checked).
- on each commit, you will generally want to:
  - add or ignore unversioned files (which files should be included versus ignored in git is a more advanced topic, but Google can help with this)
  - delete missing files (assuming this was your intent)
  - ensure all files are checked and have the correct action
- once you are ready to commit, click `Commit & Push` at the bottom.  If your button only says `Commit`, click the down arrow and choose `Commit & Push`.
- the commit action will write the changes to the git database on your local working copy, and the push action will push all commits (including this new one) to the corresponding branch on the cloud
- at this point, others will be able to go onto your branch on GitHub and see your changes
- **note that this Commit screen is very useful even if you don't want to commit yet (e.g. for reverting files, checking for changes, etc)

### Reverting / abandoning my changes to a file

- right-click your working copy in Windows Explorer, and click `Git Commit` (we are not actually committed, but we will see all our changes here to review and revert them)
- you will see a window showing all files on your working copy that are different from the rev that you are pointed at
- at this point, you can either:
  - right-click the file you want to revert / undo changes, and revert the entire file
  - double-click the file, and review and revery one line at a time by right-clicking the line you want to edit and choosing an action.

### Creating a Pull Request once the commits / revs on my branch are ready to merge into `main` branch

- ensure your working copy is clean (no uncommitted local changes, i.e. the Git Commit screen says no changes are pending).
- ensure your branch is pushed to the cloud (see above).  You can do a `Git Push` at any time just to make sure.
- go to GitHub in a browser, and browse to the main repo (https://github.com/EMI-RnD/Rain_Logger)
- click on the `X branches` link (top middle), and view the list of all branches in the cloud.
- if you have pushed the latest version of your local code, then your branch will be listed there and will have your latest code in it.  For the 2 numbers listed on your branch, ensure the left number is 0 (i.e. your branch is 0 revs behind `main` branch, meaning `main` branch doesn't have new changes that you haven't merged.)  If the left number is not zero, merge `main` into your branch (see below).  If it is 0, click the `New Pull Request` button next to your branch.
- enter a short name for your pull request, and a more detail description below on exactly what issues and missing features you solved in this PR.  Also include anything debatable in your solution, in case that will need to be discussed before the PR is merged.
- add reviewers to your PR on the top right, and set yourself as the Assignee.  Add any labels that are applicable.
- when these fields are filled out, click the `Create Pull Request` button.

### Merging changes on `main` branch into your branch (i.e. when some else merges a PR while you have a branch going, and you want to pull these changes into your branch before issuing a PR)

- if there are changes to the `main` branch that you don't have in your working copy (e.g. someone else's PR), you will have to pull the latest changes into your local `main` branch, merge these into your branch, and then do another `Git Push` to push your updated branch back to GitHub:
- if you have established that `main` has changes you need (see above, and if the left number is not 0):
- ensure your changes are committed and pushed (see above)
- right-click your working copy in Windows Explorer, and click `Git Switch/Checkout...`
- select the branch named `main`, and click OK.
- your working copy is now pointed at your local `main` branch, although there may be changes in the cloud that you don't have.
- right-click your working copy in Windows Explorer, and click `Git Pull...`, and click OK.
- your local `main` branch now has all changes from the cloud
- right-click your working copy in Windows Explorer, and click `Git Switch/Checkout...`
- select your branch, and click OK.
- right-click your working copy in Windows Explorer, and click `Merge`
- ensure the branch in the From category is `main`, then click OK.
- if you don't get any errors, then all changes from your local `main` branch have now been merged into your branch.  It would be a very good idea to do at least a quick build and test on the combined code before proceeding with your PR.
- if you get a merge conflict warning, then that means that the changes in `main` branch conflict with yours (i.e. you edited the same line on the same file).  You will need to manually merge these changes (see below).  If you are newer to git, this is a good time to call over someone nearby who is experienced in git, and errors resulting in merge conflicts can make a big mess.  You can see here (https://tortoisegit.org/docs/tortoisegit/tgit-dug-conflicts.html) for instructions.  I (Nathan Wiebe) am happy to help, although this might be easier said than done in real-time due to time zones.

### Items beyond the scope of this walk-through

- a number of items are not covered in this walkthrough.  For those items, either refer to here (https://tortoisegit.org/docs/tortoisegit/tgit-dug.html), or ask Nathan Wiebe or another dev to add a section here.
- merge conflict resolution (see https://tortoisegit.org/docs/tortoisegit/tgit-dug-conflicts.html)

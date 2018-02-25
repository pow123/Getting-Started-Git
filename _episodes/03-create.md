---
title: Creating and Tracking with Git
teaching: 20
exercises: 20
questions:
- "Where does Git store information?"
- "How do I record changes in Git?"
- "How do I record notes about what changes I made and why?"
objectives:
- "Create a local Git repository."
- "Go through the modify-add-commit cycle for one or more files"
keypoints:
- "`git init` initializes a repository."
- "Git stores all of it's repository data in the `.git` directory."
---


Let's use Git now that it's been configured. We’ll do our work in the `SWC_spring2018` folder. Check where you are using `pwd`. To change your working directory, use the `cd` command.
```shell
cd SWC_spring2018
```

To start with, let's make a new folder `git_test` in the `SWC_spring2018` directory.

Let’s create a directory for our work and then move into that directory. Suppose you started working on your thesis. Create a directory within `git_test`. 
```shell
#go to git_test
cd git_test

#make folder
$ mkdir Thesis

#go into Thesis folder
$ cd Thesis

#check Thesis contents (list files)
$ls
```

There is nothing, as expected. To show hidden files, add the flag `-a`.
```shell
$ ls -a 
./  ../ 
```
At this point we have the expected output. Let's make a new file in this folder, say a file for thesis notes. The file, titled "notes.txt" will contain the text "Chapter 1 notes.
```shell
$ echo "Chapter 1 notes" > notes.txt

#Now, listing contents, we see the added file.
$ ls
notes.txt
```
Let's read the contents of the file with the `cat` command.
```shell
$ cat notes.txt
```
We can ask now if our new file, `notes.txt` is being tracked. We can do this with `git status` command.
```shell
$ git status
fatal: Not a git repository (or any of the parent directories): .git
```
This message means that `Thesis` folder is not under the control of Git, and none of the documents within this folder are being tracked.

To place a folder under Git control, we need to initialize our `Thesis` folder to make it a repository—a place where Git can store versions of our files:

```shell
#check that you are in Thesis
$ pwd

#initialize Thesis directory with Git
$ git init
Initialized empty Git repository in .../Thesis/.git/

#check contents to see the added directory
$ ls -a
./  ../  .git/  notes.txt
```
The folder (in this case, Thesis) that contains .git sub-directory is called ***repository***. Git uses this (.git) special sub-directory to store all the information about the project, including all files and sub-directories located within the project’s directory. If we ever delete the .git sub-directory, we will lose the project’s history.

We can check that everything is set up correctly by asking Git to tell us the status of our project. Let's try the `git status` command now.
```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```
You can see that initializing a directory makes it visible to Git. 

> ## Activity 3A: Places to Create Git Repositories
> Along with tracking information for your Thesis (the project we have already created), say one would also like to track > information about each chapter. Despite a collaborator's concerns, you create a Ch1 project inside your Thesis project with the following sequence of commands:
> ~~~
> $ cd             # return to home directory
> $ cd Thesis    # go into Thesis directory, which is already a Git repository
> $ ls -a          # ensure the .git sub-directory is still present in the Thesis directory
> $ mkdir Ch1    # make a sub-directory Thesis/Ch1
> $ cd Ch1       # go into Ch1 sub-directory
> $ git init       # make the Ch1 sub-directory a Git repository
> $ ls -a          # ensure the .git sub-directory is present indicating we have created a new Git repository
> ~~~
>{: .bash}
> Is the `git init` command, run inside the `Ch1` sub-directory, required for 
> tracking files stored in the `Ch1` sub-directory?
> 
> > ## Solution
> >
> > No. You don't need to make the `Ch1` sub-directory a Git repository 
> > because the `Thesis` repository will track all files, sub-directories, and 
> > sub-directory files under the `Thesis` directory.  Thus, in order to track 
> > all information about Ch1, you only needed to add the `Ch1` sub-directory
> > to the `Thesis` directory.
> > 
> > Additionally, Git repositories can interfere with each other if they are "nested" in the
> > directory of another: The outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
> ## Correcting `git init` Mistakes
> Since a nested repository is redundant and may cause confusion down the road, you would like to remove the nested repository. How can you undo your last `git init` in the `Ch1` sub-directory?
>
> > ## Solution -- USE WITH CAUTION!
> >
> > To recover from this little mistake, just remove the `.git` folder in the Ch1 sub-directory by running the following command from inside the 'Ch1' directory:
> >
> > ~~~
> > $ rm -rf Ch1/.git
> > ~~~
> > {: .bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire git-history of a project you might want to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}


If you are still in `Ch1`, navigate back to `Thesis` using the `cd` command. Now Git tells us what files are in the directory and what is their status. In our case, Git says that there is a notes.txt file and it is not tracked. The “untracked files” message means that there’s a file in the directory that Git isn’t keeping track of.  Git also tells us that we need to use `git add` command to start tracking this file:
```
$ git add notes.txt

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   notes.txt
```
The current version of `notes.txt` is now ready (or staged) to be recorded by Git. If we check the status of our project again (`git status`), Git tells us that it’s noticed the new file. To record the current version of notes.txt, `git commit` command is used.
```
#commit changes
$ git commit -m "Start notes for Thesis"

[master (root-commit) 76604e5] first note
 1 file changed, 1 insertion(+)
 create mode 100644 notes.txt
```
Git insists that we add files to the set we want to commit before actually committing anything. This allows us to commit our changes in stages and capture changes in logical portions rather than only large batches. For example, suppose we’re adding a few citations to relevant research to our thesis. We might want to commit those additions, and the corresponding bibliography entries, but not commit some of our work drafting the conclusion (which we haven’t finished yet).

To allow for this, Git has a special staging area where it keeps track of things that have been added to the current changeset but not yet committed. When we run `git commit`, Git takes everything we have told it to save by using `git add` and stores a copy permanently inside the special `.git` directory. This permanent copy is called a [commit]({{ page.root }}/reference/#commit)
(or [revision]({{ page.root }}/reference/#revision)) and its short identifier is 76604e5 (Your commit may have another identifier.)


We use the -m flag (for “message”) to record a short, descriptive, and specific comment that will help us remember later on what we did and why. If we just run `git commit` without the -m option, Git will launch BBEdit (or whatever other editor we configured as core.editor) so that we can write a longer message.

Good commit messages start with a brief (<50 characters) summary of changes made in the commit. If you want to go into more detail, add a blank line between the summary line and your additional notes.

Now run `git status` again. 
```
#check satus
$ git status
On branch master
nothing to commit, working tree clean
```
Everything is up to date! 

You can check the history of your commits with `git log`. This command lists all commits made to a repository in reverse chronological order. The listing for each commit includes the commit’s full identifier (which starts with the same characters as the short identifier printed by the git commit command earlier), the commit’s author, when it was created, and the log message Git was given when the commit was created:
```
$ git log

commit 76604e57022d52b2ebf3c92d0f5358354850fa37 (HEAD -> master)
Author: pow123 <peace@uta.edu>
Date:   Sun Feb 24 15:15:00 2018 -0600

    Start notes for Thesis
    
#or for a faster view
$ git log --oneline
```
In summary, here are the steps that must be completed to track changes in your documents with Git.

- [x] Initialize your folder with `git init` command. This is done only **one** time for every new parent directory
- [x] Prepare new/modified files for saving(committing) with `git add` command
- [x] Create a permanent copy of your new/modified file with `git commit -m "message" `


![](http://swcarpentry.github.io/git-novice/fig/git-staging-area.svg)


> ## Activity 3B: Adding and Tracking Changes
> Open notes.txt in text editor and add the following line of text to it: "Chapter 2 notes"
> Save your changes and track your changes with Git.
> 
> > ## Solution
> >
> > Open `notes.txt`, add the text, save and close. (Or, from the command line, type `open -t notes.txt` to open it in BBEdit.
> > When we run git status now, it tells us that a file it already knows about has been modified. You can also see your new additions to `notes.txt` with `cat`:
> > ~~~
> > $ cat notes.txt
> > Chapter 1 notes
> > Chapter 2 notes
> >
> > $ git status
> > On branch master
> > Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
> >
> >   modified:   notes.txt
> >
> > no changes added to commit (use "git add" and/or "git commit -a")
> > ~~~
> > {: .bash}
> > The last line is the key phrase: “no changes added to commit.” We have changed this file, 
> > but we haven’t told Git we will want to save those changes (which we do with `git add`) 
> > and we haven't saved them (which we do with `git commit`). So let’s do that now:
> > ~~~
> > $ git add notes.txt
> > $ git commit -m "added ch 2 notes"
> > ~~~
> > {: .bash}
> {: .solution}
{: .challenge}
  
Now, run `git log`.  The output of `git log` tells you the history of your changes. Your commit messages are very important, in case you want to restore an old version of the document, they will help you to pick out the version you want.

Your versions (or commits) have unique identifiers. In addition, the most recent version can be identified by `HEAD`. It is also good practice to always review changes before saving them. We do this using `git diff`. This shows us the differences between the current state of the file and the most recently saved version:
```shell
#you can specify only first few characters of the commit identifier.
$ git diff 76604e5 HEAD notes.txt
```
 
Now, let's see how to turn an existing directory into a git repository. You might want to track files for some of your existing projects. Let's create a new directory: `git_github` in the `SWC_spring2018` folder. How will you place this directory under Git control?

```
#Go to git_github
$ cd ../../git_github

#Or type the path directly
$ cd ~/Desktop/SWC_spring2018/git_github

#initialize
$ git init

#check status
$ git status

#prepare files for tracking
$ git add .

#commit changes 
$ git commit -m "added git_github directory"

#check commit history
$ git log
```

Now every file in this directory is being tracked. Notice that we added multiple folders and files in the same commit. If you want to know what files were included in this commit:
```
# print the list of files that are part of a given commit
$ git show --name-only 8af5f83
```
As you continue working on this project, you will be adding new directories and files to it. 
Let's try it.

> ## Activity 3C: Tracking File Changes
> Make a file called git_steps.txt inside `git_github`. 
> Record `git` commands you must use to start tracking your changes.
> Save this file and commit `git_github` directory to Git.
> 
> NOTE:`git init` should only be run one time in the root directory of your project. 
{: .challenge}
 
> ## Activity 3D: Committing Multiple Files
>
> The staging area can hold changes from any number of files
> that you want to commit as a single snapshot.
>
> 1. Add some text to `git_steps.txt`.
> 2. Create a new file `github_steps.txt` and add text there.
> 3. Add changes from both files to the staging area,
> and commit those changes.
>
> > ## Solution
> >
> > First we add to  `git_steps.txt` then we create `github_steps.txt`:
> > ~~~
> > $ open -t git_steps.txt
> > $ cat git_steps.txt
> > ~~~
> > {: .bash}
> > ~~~
> > Steps to using Git
> > ~~~
> > {: .output}
> > ~~~
> > $ echo "Steps to using GitHub" > github_steps.txt
> > $ cat github_steps.txt
> > ~~~
> > {: .bash}
> > ~~~
> > Steps to using GitHub
> > ~~~
> > {: .output}
> > Now you can add both files to the staging area. We can do that in one line:
> >
> > ~~~
> > $ git add git_steps.txt github_steps.txt
> > ~~~
> > {: .bash}
> > Or with multiple commands:
> > ~~~
> > $ git add git_steps.txt
> > $ git add github_steps.txt
> > ~~~
> > {: .bash}
> > Now the files are ready to commit. You can check that using `git status`. If you are ready to commit use:
> > ~~~
> > $ git commit -m "Added steps for Git and GitHub"
> > ~~~
> > {: .bash}
> > ~~~
> > [master e6a7d94] Added steps for Git and GitHub
> >  2 files changed, 2 insertions(+)
> >  create mode 100644 git_steps.txt
> >  create mode 100644 github_steps.txt
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## Optional Activity: Modifying Files
>
> * Write a three-line biography for yourself in a file called `about_me.txt`,
> commit your changes
> * Modify one line, add a fourth line
> * Display the differences
> between its updated state and its original state.
> 
> > ## Solution
> >
> > Create your biography file `about_me.txt` using `BBEdit` or another text editor.
> > ~~~
> > $ git add about_me.txt
> > $ git commit -m'Adding biography file'
> > ~~~
> > {: .bash}
> >
> > Modify the file as described (modify one line, add a fourth line).
> > To display the differences
> > between its updated state and its original state, use `git diff`:
> >
> > ~~~
> > $ git diff about_me.txt
> > ~~~
> > {: .bash}
> >
> {: .solution}
{: .challenge}

> ## Optional: Author and Committer
>
> For each of the commits you have done, Git stored your name twice.
> You are named as the author and as the committer. You can observe
> that by telling Git to show you more information about your last
> commits:
>
> ~~~
> $ git log --format=full
> ~~~
> {: .bash}
>
> When committing you can name someone else as the author:
>
> ~~~
> $ git commit --author="Anne Example <anne@example.net>"
> ~~~
> {: .bash}
>
> Create a new repository and create two commits: one without the
> `--author` option and one by naming a colleague of yours as the
> author. Run `git log` and `git log --format=full`. Think about ways
> how that can allow you to collaborate with your colleagues.
>
> > ## Solution
> >
> > ~~~
> > $ git add about_me.txt
> > $ git commit -m "Update my bio." --author="Anne Example <anne@example.net>"
> > ~~~
> > {: .bash}
> > ~~~
> > [master 963e793] Update my bio.
> > Author: Anne Example <anne@example.net>
> > 1 file changed, 2 insertions(+), 2 deletions(-)
> >
> > $ git log --format=full
> > commit 963e7931f16d91f1559197cb91d819fb87ca06e1
> > Author: Author: Anne Example <anne@example.net>
> > Commit: pow123 <peace@uta.edu>
> >
> > Update my bio.
> >
> > commit aaa3271e5e26f75f11892718e83a3e2743fab8ea
> > Author: pow123 <peace@uta.edu>
> > Commit: pow123 <peace@uta.edu>
> >
> > My initial bio.
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

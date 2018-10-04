---
title: Exploring History
teaching: 15
exercises: 0
questions:
- "How can I identify old versions of files?"
- "How do I review my changes?"
- "How can I recover old versions of files?"
objectives:
- "Explain what the HEAD of a repository is and how to use it."
- "Identify and use Git commit numbers."
- "Compare various versions of tracked files."
- "Restore old versions of files."
keypoints:
- "`git diff` displays differences between commits."
- "`git checkout` recovers old versions of files."
---


The clear advantage of tracking your documents with Git is that you can always go back to the previous version. Let's see how this works.

The output of `git log` provides all the information you need to retrieve the older version of the document.

Let's modify our `git_steps.txt` and add a note to it:

```
$ echo "Use git init only one time for every project" >>git_steps.txt

$ cat git_steps.txt

$ git add .
$ git commit -m "added note to git_steps.txt"

#view latest version
$ cat git_steps.txt
```
Now, this is our second version of git_steps.txt. Our first version was stored when we first created the file, and our second version when we added a new line to it.

Suppose that some time later, you want the original version of git_steps.txt. How would you do that?

To restore any of the original versions of the document, you use `git checkout` command:
```
#general syntax
$ git checkout <commitID> <file>
```

If we want the original git_steps.txt:
```
#see what commitID is associated with the original version
git log --oneline

#the commit that includes original file has message "Added steps for Git and GitHub" (or whatever you used when you committed the change)
$ git checkout e6a7d94 git_steps.txt
```

Now let's make sure that we have original version of git_steps.txt
```
#view restored version
$ cat git_steps.txt

#restored version has not been committed, see HEAD commit
$ git log

#see what to do next
$ git status

#If you decide to go ahead with restoring file, commit the change since checkout command places file in the staging area (no need for 'git add')

$ git commit -m "changed to the original git_steps.txt version"

$ git status

#see HEAD now
$ git log

#if you run `git checkout, but would like to cancel restoring the old version:
#unstage restored file
$ git reset HEAD git_steps.txt 

#return to latest version before you attempted to restore the file
$ git checkout -- git_steps.txt

#see current file
$ cat git_steps.txt
```

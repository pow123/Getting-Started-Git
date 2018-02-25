---
title: Collaborating
teaching: 5
exercises: 5
questions:
- "How can I use version control to collaborate with other people?"
objectives:
- "Clone a remote repository."
- "Collaborate pushing to a common repository."
keypoints:
- "`git clone` copies a remote repository to create a local repository with a remote called `origin` automatically set up."
---


This part of the lesson is modified from this [Source](https://help.github.com/articles/creating-a-pull-request-from-a-fork/)

You can contribute to whatever project you like. Suppose you would like to add a new feature to someone else's project. You can always propose your changes; in GitHub language, this is known as  `pull request`.

Steps for making pull requests (or PRs):

- go to the project you want to contribute to
  (https://github.com/AnnaWilliford/SWC_Spring2018_lessons)

- copy the project to your GitHub account by clicking `fork` button on the top right corner of the page.

You should now have a new repository called `SWC_Spring2018_lessons` in **YOUR** account. You can now copy other projects/repositories to your GitHub account!

You can also copy a remote repository to the local machine, let's say, to the Desktop. From your local terminal, type:
```
$ git clone https://github.com/YourUsername/SWC_2018-02-25.git ~/Desktop/SWC_Spring2018_lessons.git
```
You now have all lessons both on your GitHub account and on your local machine! And, of course, you have access to any public repository on GitHub in a similar way.

Now, what is even better, you can contribute to the project you forked/cloned(copied) by suggesting changes to the documents in the repository. If, for example, you find a better way to explain some topic we were covering in this workshop, you can make changes to the lessons locally on your machine and then send a `pull request` to the owner of repository. The owner will review your changes and decide to accept(merge) proposed changes or reject them.

> ## Want to try?
> Go to `SWC_Spring2018_lessons` repo on your local machine and open a new topic branch for the project:
> ```
> $ git checkout -b YourName
> ```
> You can now modify and add anything you want in this project. When ready with your final contributions, you will be able to send your pull request.
> 
> For example, add your create new file.
> ```
> #create new file
> $ git add .
> $ git commit -m "add new file"
> 
> #Push your topic branch up to your fork:
> $ git push origin YourName
> ```
> Go to the forked repo on your GitHub account and click on the green `compare & pull request` button
> 
> A bit more terminology here: 
> `base fork` is the repository you'd like to merge changes into. Use the `base branch` drop-down menu to select the branch of the upstream repository you'd like to merge changes into.
> 
> Use the `head fork` drop-down menu to select your fork, then use the compare branch drop-down menu to select the branch you made your changes in.

> Type a title and description for your pull request.
> 
> Click `Create pull request`
> 
> The owner of repository will get notification about pull request and will review your proposed changes.
{: .callout}

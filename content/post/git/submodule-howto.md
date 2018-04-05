---
title: "Git Submodule: howto"
date: "2018-04-03T17:38:02-04:00"
categories:
  - git
  - howto
tags:
  - git
draft: "false"
keywords:
  - git
  - submodule
thumbnailImagePosition: left
thumbnailImage: https://git-scm.com/images/logos/downloads/Git-Icon-Black.png
---

Often it is extremely helpful to embed one git repository into another.  An example that comes to mind is when you want to vendor dependencies for a project.  This is where `git submodule` comes in.  The submodule command clones one repo into a sub-directory controlled by another git repository.  Git still controls version control over both repositories (master and embedded) and allows you to easily pin the embedded repository to a specific commit, version, or branch.

The issue of copying the embedded repository into a sub-directory of the master repository is all handled by git.  So no constant checking the embedded repository for changes and manually downloading files that have changed.  Each repository is treated as separate entities so commits should never cause merge issues.

Setting up a submodule in a project is broken down into just a few steps

1. Add submodule
2. Add & Commit
3. Update submodule

{{< hl-text yellow >}}
Update submodule is a task that will need to be performed whenever there is an update to the embedded repository that you would like to add.
{{< /hl-text >}}

## Add submodule

To add a new submodule you use the `git submodule add` command with the URL of the project you would like to embed.

{{< codeblock lang="bash" >}}
$ git submodule add https://github.com/chaconinc/DbConnector
Cloning into 'DbConnector'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
{{< /codeblock >}}

## Add & Commit

You commit changes to a repository with submodules the same way you would any other repository.

{{< codeblock lang="bash" >}}
$ git commit -am 'added DbConnector module'
[master fb9093c] added DbConnector module
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 DbConnector
{{< /codeblock >}}

## Update submodule

To update a submodule you will need to run `git submodule update --remote`.  When this is ran git will do a `git fetch` and `git merge` on all of the submodules listed in the `.gitmodules` file.

{{< codeblock lang="bash" >}}
$ git submodule update --remote
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 2), reused 4 (delta 2)
Unpacking objects: 100% (4/4), done.
From https://github.com/chaconinc/DbConnector
   3f19983..d0354fc  master     -> origin/master
Submodule path 'DbConnector': checked out 'd0354fc054692d3906c85c3af05ddce39a1c0644'
{{< /codeblock >}}

## Additional Information

There is a whole lot of detail that I did not go into in this post.  I really just wanted something that I could reference quickly down the road, so I picked the tasks that I find myself performing most often.

If you would like more depth you should really check out https://git-scm.com/book/en/v2/Git-Tools-Submodules
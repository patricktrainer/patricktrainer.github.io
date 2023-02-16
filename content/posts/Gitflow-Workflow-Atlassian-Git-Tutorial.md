---
date: '2023-02-16'
draft: false
title: Gitflow-Workflow-Atlassian-Git-Tutorial
---

# Gitflow-Workflow-Atlassian-Git-Tutorial

A simple way to do this is for one developer to create an empty `develop` branch locally and push it to the server:
```
git branch develop
git push -u origin develop
```
This branch will contain the complete history of the project, whereas `master` will contain an abridged version.
Other developers should now clone the central repository and create a tracking branch for `develop.`
When using the git-flow extension library, executing `git flow init` on an existing repo will create the `develop` branch:
```
$ git flow init
Initialized empty Git repository in ~/project/.git/
No branches exist yet.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]
How to name your supporting branch prefixes?
Without the git-flow extensions:
```
git checkout develop
git checkout -b release/0.1.0
```
When using the git-flow extensions:
```
$ git flow release start 0.1.0
Switched to a new branch 'release/0.1.0'
```
Once the release is ready to ship, it will get merged it into `master` and `develop`, then the `release` branch will be deleted.
To finish a `release` branch, use the following methods:
Without the git-flow extensions:
```
git checkout master
git merge release/0.1.0
```
Or with the git-flow extension:
```
git flow release finish '0.1.0'
```
## Hotfix Branches
!
A `hotfix` branch can be created using the following methods:
Without the git-flow extensions:
```
git checkout master
git checkout -b hotfix_branch
```
When using the git-flow extensions:
```
$ git flow hotfix start hotfix_branch
```
Similar to finishing a `release` branch, a `hotfix` branch gets merged into both `master` and `develop.`
```
git checkout master
git merge hotfix_branch
git checkout develop
git merge hotfix_branch
git branch -D hotfix_branch
```
```
$ git flow hotfix finish hotfix_branch
```
## Example
A complete example demonstrating a Feature Branch Flow is as follows.
```
git checkout mastergit checkout -b developgit checkout -b feature_branch# work happens on feature branchgit checkout developgit merge feature_branchgit checkout mastergit merge developgit branch -d feature_branch
```
In addition to the `feature` and `release` flow, a `hotfix` example is as follows:
```
git checkout master
git checkout -b hotfix_branch
# work is done commits are added to the hotfix_branch
git checkout develop
git merge hotfix_branch
git checkout master
git merge hotfix_branch
```
## Summary
Here we discussed the Gitflow Workflow.

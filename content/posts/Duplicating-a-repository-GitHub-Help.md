---
 	layout: post
 	title: Duplicating-a-repository-GitHub-Help
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# Duplicating-a-repository-GitHub-Help# Duplicating a repository - GitHub Help
Created: January 30, 2020 8:55 PM
URL: https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository
[GitHub.com](https://help.github.com/en/github) [Creating, cloning, and archiving repositories](https://help.github.com/en/github/creating-cloning-and-archiving-repositories) [Creating a repository on GitHub](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github) [Duplicating a repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
# Duplicating a repository
To duplicate a repository without forking it, you can run a special clone command, then mirror-push to the new repository.
[Mac](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository) [Windows](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository) [Linux](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
### [In this article](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
- [Mirroring a repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
- [Mirroring a repository that contains Git Large File Storage objects](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
- [Mirroring a repository in another location](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
Before you can duplicate a repository and push to your new copy, or *mirror*, of the repository, you must [create the new repository](https://help.github.com/en/articles/creating-a-new-repository) on GitHub.
Open Terminal.
```
old-repository
```
### [Mirroring a repository that contains Git Large File Storage objects](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
1.
Replace the example username with the name of the person or organization who owns the repository, and replace the example repository name with the name of the repository you'd like to duplicate.
Push the repository's Git Large File Storage objects to your mirror.
```
old-repository
```
### [Mirroring a repository in another location](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/duplicating-a-repository)
If you want to mirror a repository in another location, including getting updates from the original, you can clone a mirror and periodically push the changes.

---
 	layout: post
 	title: 3-Ways-to-Change-a-Users-Default-Shell-in-Linux
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# 3-Ways-to-Change-a-Users-Default-Shell-in-Linux# 3 Ways to Change a Users Default Shell in Linux
Created: April 26, 2020 11:45 PM
URL: https://www.tecmint.com/change-a-users-default-shell-in-linux/
In this article, we will describe how to change a user’s shell in Linux.
**Read Also**: [5 Most Frequently Used Open Source Shells for Linux](https://www.tecmint.com/different-types-of-linux-shells/)
There are several reasons for changing a user’s shell in Linux including the following:
1.
When creating user accounts with the [useradd or adduser](https://www.tecmint.com/add-users-in-linux/) utilities, the `--shell` flag can be used to specify the name of a user’s login shell other than that specified in the respective configuration files.
### 1. usermod Utility
[usermod](https://www.tecmint.com/usermod-command-examples/) is a utility for modifying a user’s account details, stored in the **/etc/passwd** file and the `-s` or `--shell` option is used to change the user’s login shell.
In this example, we’ll first check user tecmint’s account information to view his default login shell and then change its login shell from **/bin/sh** to **/bin/bash** as follows.
[3%20Ways%20to%20Change%20a%20Users%20Default%20Shell%20in%20Linux%207f26076b89524234a53cc7c75eb29d7e/Change-User-Shell-using-Usermod.png](3%20Ways%20to%20Change%20a%20Users%20Default%20Shell%20in%20Linux%207f26076b89524234a53cc7c75eb29d7e/Change-User-Shell-using-Usermod.png)
Change User Shell using Usermod
### 2. chsh Utility
**chsh** is a command line utility for changing a login shell with the `-s` or **–shell** option like this.
Change User Shell in /etc/passwd File
In this method, simply open the **/etc/passwd** file using any of your favorite command line text editors and change a specific users shell.

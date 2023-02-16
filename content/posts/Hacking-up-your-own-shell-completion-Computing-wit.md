---
date: '2021-01-01'
draft: false
tags: '[]'
title: Hacking-up-your-own-shell-completion-Computing-wit
---

# Hacking-up-your-own-shell-completion-Computing-wit

I’ve often used `fzf` as a file finder, you can simply run something like `git ls-files | fzf`, and pass the output to your editor, and you’ve already made a git aware fuzzy file finder, running this inside your editor like [fzf-vim](https://github.com/junegunn/fzf.vim) makes this even more powerful.
One quick solution to our `doer` problem is to write a bash script like this:
```
#!/bin/bash
doer $(doer -list | fzf)
```
Here we just use command substitution to run `doer`’s list command, pass it to `fzf`, then run doer with the result.
Okay fine, I guess I can add proper shell completion to the command using `fish`’s built in `complete` command, add it to the repo, and set up an install script.
What if there was a way to strap an `fzf` completion thing into my shell, that I fully control through just a couple lines of `fish` script, that doesn’t interfere with built-in completion, and allows me to quickly add bindings to any command I frequently run?
```
function fzf-smart-completion -d "List files and folders"
set -l commandline (__fzf_parse_commandline)
set -l dir $commandline[1]
set -l fzf_query $commandline[2]
# use our cool new completion checker
set -l FZF_CMD (get-completion-command); or return
# fzf edge case and formatting (prevents fzf from taking up the whole screen)
set FZF_HEIGHT 40%
begin
set -lx FZF_DEFAULT_OPTS "--height $FZF_HEIGHT --reverse $FZF_DEFAULT_OPTS $FZF_CMD[2]"
eval "$FZF_CMD[1] | "(__fzfcmd)' -m --query "'$fzf_query'"' | while read -l r; set result $result $r; end
end
if [ -z "$result" ]
commandline -f repaint
return
else
# Remove last token from commandline.
commandline -t ""
end
for i in $result
commandline -it -- (string escape $i)
commandline -it -- ' '
end
commandline -f repaint
end
bind -M insert \et fzf-smart-completion
bind \et fzf-smart-completion
```
With this little bit of `fish` scripting, we now have a pretty cool `ALT-T` command that runs our own fuzzy autocomplete like so.
```
function get-completion-command
set -l cmd (commandline)
switch $cmd
case 'doer *'
echo 'doer -list'
case 'go test *'
echo 'git ls-files | grep _test.go'
case 'yarn test *'
echo 'git ls-files | grep .test.ts'
case '*'
return 1
end
end
```
You can see the go tester in action here:
Another useful thing I’ve found is automating some routine `git` commands.

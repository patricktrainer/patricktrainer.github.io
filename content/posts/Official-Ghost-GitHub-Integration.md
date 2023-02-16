---
date: '2023-02-16'
draft: false
title: Official-Ghost-GitHub-Integration
---

# Official-Ghost-GitHub-Integration

# Official Ghost + GitHub Integration
Created: April 23, 2020 2:28 PM
URL: https://ghost.org/integrations/github/
Set up simple continuous integration of your Ghost theme to deploy directly to your Ghost website with [GitHub Actions](https://github.com/features/actions).
## Use GitHub Actions to deploy your theme
GitHub Actions allow you to build simple automation on top of any repository, including running a build command on a theme and pushing the compiled zipfile to the Ghost Admin API.
[Official%20Ghost%20+%20GitHub%20Integration%205b27867598de4daa9a3b11611b3d6958/image-1.png](Official%20Ghost%20+%20GitHub%20Integration%205b27867598de4daa9a3b11611b3d6958/image-1.png)
### Set your Ghost integration credentials in GitHub
Next, copy and paste your integration details into your GitHub repository's environment variables.
Copy and paste the following code into a new file in your repository under `.github/workflows/main.yml` - this will automatically use the official [Ghost GitHub Action](https://github.com/marketplace/actions/deploy-ghost-theme) from GitHub's Marketplace:
```
name: Deploy Theme
on:
push:
branches:
- master
jobs:
deploy:
runs-on: ubuntu-18.04
steps:
- uses: actions/checkout@master
- uses: TryGhost/action-deploy-theme@v1.0.0
with:
api-url: ${{ secrets.GHOST_ADMIN_API_URL }}
api-key: ${{ secrets.GHOST_ADMIN_API_KEY }}
```
Now, every time you push changes to your theme repository, your theme will automatically build and deploy to Ghost Admin.
## Use Github Gists to share code snippets
[GitHub Gists](https://gist.github.com/) are a simple way of sharing code snippets with other developers.
[Official%20Ghost%20+%20GitHub%20Integration%205b27867598de4daa9a3b11611b3d6958/Creating-a-Gist.png](Official%20Ghost%20+%20GitHub%20Integration%205b27867598de4daa9a3b11611b3d6958/Creating-a-Gist.png)
To share a Gist in Ghost, locate the embed option from the dropdown in the top navigation and copy the HTML embed code to your clipboard:
!
[Official%20Ghost%20+%20GitHub%20Integration%205b27867598de4daa9a3b11611b3d6958/Gist-embed-code-1.png](Official%20Ghost%20+%20GitHub%20Integration%205b27867598de4daa9a3b11611b3d6958/Gist-embed-code-1.png)
### Paste it into a HTML card in the editor
Create a new HTML block in the Ghost editor on the post you would like to embed your code snippet and paste in the embed code.

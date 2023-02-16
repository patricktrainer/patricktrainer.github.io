
---
    title: Ghost-Theme-Development-Using-Visual-Studio-Code-R
    date: 2021-01-01    
    draft: true
    tags: []
---
# Ghost-Theme-Development-Using-Visual-Studio-Code-R# Ghost Theme Development Using Visual Studio Code Remote Development With Containers
Created: April 19, 2020 12:54 PM
URL: https://geeklearning.io/visual-studio-code-remote-development-ghost-theme-with-containers/
Earlier, I've introduced [Visual Studio Remote Developmen](https://geeklearning.io/introduction-to-visual-studio-code-remote-development/)t and you might be wondering what a practical use case would be.
Here is a quick description of the steps it was running:
- Build the theme
- Copy it to a `.staging` directory
- Start a docker container with the database mounted to a `.data` and `.staging` mounted in the theme directory
- Watch for file changes, and repeat the step above.
We will customize it as follow:
- Install Yarn so we can restore the theme dev dependencies
- Install `gscan` so we can validate our theme easily
- Configure `bash` as the default shell (who uses sh these days?
`.devontainer/Dockerfile`:
```
FROM ghost
# Configure apt
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
&& apt-get -y install --no-install-recommends apt-utils 2>&1
# Verify git and process tools are installed
RUN apt-get install -y git procps
# Remove outdated yarn from /opt and install via package
# so it can be easily updated via apt-get upgrade yarn
RUN rm -rf /opt/yarn-* \
&& rm -f /usr/local/bin/yarn \
&& rm -f /usr/local/bin/yarnpkg \
&& apt-get install -y curl apt-transport-https lsb-release \
&& curl -sS https://dl.yarnpkg.com/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/pubkey.gpg | apt-key add - 2>/dev/null \
&& echo "deb https://dl.yarnpkg.com/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
&& apt-get update \
&& apt-get -y install --no-install-recommends yarn
RUN yarn global add gscan
# Clean up
RUN apt-get autoremove -y \
&& apt-get clean -y \
&& rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog
ENV SHELL /bin/bash
ENV url http://localhost:3001
```
## Visual Studio Code configuration
Visual Studio Code needs a `devcontainer.json` file to be able to understand what to do with you dockerfile.
`.devontainer/devcontainer.json`:
```
{
"dockerFile": "Dockerfile",
"extensions": [],
"appPort": [
"3001:2368"
],
"postCreateCommand": "ln -s /workspaces/geek-learning-io-casper/.data /var/lib/ghost/content/data && yarn install --production=false"
}
```
## Tweaking the gulp file
This step has nothing to do with Remote development and is only related to the ghost use case.
```
yarn add ps-list @tryghost/admin-api --dev --production=false
```
In `gulpfile.js` we will add the following imports:
```
const psList = require('ps-list');
const adminApiClient = require("@tryghost/admin-api");
const fs = require('fs');
const path = require('path');
```
Then we will replace the end section of the file with the following:
```
async function ghost() {
var exec = require("child_process").exec;
const processes = await psList();
const ghostProcess = processes.filter(x => x.cmd == "/usr/local/bin/node current/index.js");
if (ghostProcess.length) {
process.kill(ghostProcess[0].pid)
}
exec(
"node current/index.js",
{ cwd: process.env.GHOST_INSTALL, env: process.env, detached: true },
function callback(error, stdout, stderr) {
}
);
};
async function deployThemeViaApi(done) {
var targetDir = 'dist/';
var themeName = require('./package.json').name;
var filename = themeName + '.zip';
const themePath = path.join(__dirname, targetDir, filename);
const url = "http://localhost:2368";
const client = new adminApiClient({
url,
key: fs.readFileSync(path.join(__dirname, '.token'), { encoding: 'utf8' }),
version: "v2"
});
await client.themes.upload({ file: themePath });
};
const cssWatcher = () => watch('assets/css/**', css);
const hbsWatcher = () => watch(['*.hbs', 'partials/**/*.hbs', '!node_modules/**/*.hbs'], hbs);
const watcher = parallel(cssWatcher, hbsWatcher);
const build = series(css, js);
const dev = series(build, serve, watcher);
const zipBuild = series(build, zipper);
const dockerCssWatcher = () => watch('assets/css/**', series(zipBuild, deployThemeViaApi));
const dockerHbsWatcher = () => watch(['*.hbs', 'partials/**/*.hbs', '!node_modules/**/*.hbs'], series(zipBuild, deployThemeViaApi));
const dockerWatcher = parallel(dockerCssWatcher, dockerHbsWatcher);
const dockerDev = series(ghost, zipBuild, deployThemeViaApi, dockerWatcher);
exports.ghost = ghost;
exports.build = build;
exports.zip = zipBuild;
exports.dev = dev;
exports.default = dockerDev;
```
This will change the default gulp task to a task designed to build, zip and deploy the theme to the blog on changes.
[Ghost%20Theme%20Development%20Using%20Visual%20Studio%20Code%20R%20cfb55d0e495b4904961745c147db7412/aziz-acharki-gXndgCS-CGo-unsplash.jpg](Ghost%20Theme%20Development%20Using%20Visual%20Studio%20Code%20R%20cfb55d0e495b4904961745c147db7412/aziz-acharki-gXndgCS-CGo-unsplash.jpg)
Now we can upgrade the readme with the steps to get started, you'll notice that the longest part has to do we initializing ghost :) :
```
To develop on the theme we recommend that you use Visual Studio Code with the Remote development tools
* Install [VS Code](https://code.visualstudio.com/)
* Install [Remote Developement Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
* Clone this Repository (if not done already)
* Open it
* Hit `Ctrl/Command + Shift + P`, type Reopen
* `Reopen Folder in container` should appear, Select and Press enter
* Wait for the container to be build and start
If it's your first time, start ghost using yarn gulp ghost
* Open a browser on `https://localhost:3001` configure your blog and your account.

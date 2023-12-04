# Setup a [[Node.js]] Dev Environment
## Installation
### Browser based installation
- go to [nodejs.org](https://nodejs.org/en)
- choose a recent LTS(long term support) version
- open the downloaded file 
- accept the terms
- installation can be verified in the terminal by typing `node --version` or `node -v`
### NVM installation
- Node can also be installed using Node Version Manager (NVM)
- this CLI tool allows you to manage multiple active [[Node.js]] versions
- install NVM from the GitHub repo [here](https://github.com/nvm-sh/nvm)
	- Note: Installation edits your terminal configuration file.  To use NVM the terminal must be closed and reloaded.
- then node can be installed using the `nvm install node` (for the latest version) or `nvm install {desired node version number}` commands
	- Examples:  `nvm install 14` or `nvm install 16`
- the `nvm use {node version number}` command is used to select a different installed version for use
## Start a Node project
- create a folder for your project
- open the folder in your editor
	- For VSCode:
		- navigate into the folder in the terminal => `code .`
		- or drag the folder into an empty VSCode window and drop
- run `npm init -y` in the terminal to initialize a new node project and create a `package.json` file
- create an app file inside your project folder
	- this can be named anything, but convention is to name it `app.js`
- run the app by typing `node {app_name}` in a terminal from the same folder (no browser or HTML required!)
	- it's easiest to use the IDE integrated terminal
VSCode tips:
- Live Preview extension

## Resources
[Fireship Node video](https://youtu.be/ENrzD9HAZK4) for beginners
[learnyounode CLI challenge program](https://github.com/workshopper/learnyounode)
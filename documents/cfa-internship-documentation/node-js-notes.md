# Node.js

## Overview
**Node.js** is a JavaScript runtime built on Chrome's V8 JavaScript engine, designed for building scalable network applications. It's known for its event-driven, non-blocking I/O model, making it efficient and suitable for diverse backend applications.
### Node.js vs Browser JavaScript

- **No Browser APIs**: Lacks DOM, geolocation, alert, and window object.
- **Filesystem & Network Access**: Offers extended capabilities compared to browser environments.
- **Version-based**: Relies on specific Node.js versions, independent of web browser updates.
- **Module System**: Utilizes CommonJS and ES6 modules, which differ from the module syntax used in browser environments.

### Node REPL (Read-Eval-Print Loop)
- Launch by typing `node` in the terminal.
- Useful for executing JavaScript code line by line for testing and debugging.
## Installation
### Installing nodejs
- The standard nodejs package includes both `node` and `npm` (node package manager) executables.
#### Standard Installation

1. Visit [nodejs.org](https://nodejs.org/en) and choose a recent LTS (Long Term Support) version.
2. Run the downloaded installer, accepting the terms.
3. Verify the installation in the terminal: `node --version` or `node -v`.

#### Using Node Version Manager (NVM)

1. Install NVM from [its GitHub repository](https://github.com/nvm-sh/nvm).
2. After installation, reopen the terminal to load the updated config file.
3. Install Node.js: `nvm install node` for the latest version, or `nvm install [version number]` for a specific version.
4. Switch between installed versions: `nvm use [version number]`.

### Initializing a new node project

- The `npm init` command will initialize a node project and create a `package.json` file where the projects dependencies are tracked.

## Fundamentals
### Variables
#### Globals
These can be accessed from anywhere in the program
- `__dirname`- path to the current directory
- `__filename` - file name
- `require` - function to use modules (CommonJS)
- `module` - info about the current module
- `process` - info about the current Node.js process
	- `process.argv`: an array that contains the command line arguments passed to the current process
	- `process.pid`: the ID of the current process
	- `process.env`: an object that contains the environment variables of the current process
	- `process.exit()`: terminates the current process with an optional exit code
- `console`
- `global`: The global namespace object, analogous to the `window` object in the browser.
- `Buffer`: A global class used to handle binary data. It is not necessary to `require('buffer')` to use it.
- `setTimeout`, `clearTimeout`, `setInterval`, `clearInterval`: Timers functions available globally, similar to browser JavaScript.

### package.json
key: value pairs that define project metadata and dependencies.
- `"name":`
- `"version":`
- `"main":`
- `"type":` - "module" for ES6 module imports
- `"bin":` - { "{command}": "{path to executable}"} defines the command to execute your program from the terminal
- `"scripts":`
- `"author":`
- `"license":`
- `"keywords":`
- `"description":`
### Modules and Imports
An app can be separated into smaller 'module' files that are imported into the main app file
Every file is a module in Node.js.  What is shared from each file is user defined so we can only share the minimum necessary.
##### Defining a files export object
- `module.exports = { {define properties here} }` (CommonJS)
- `export default {}` (ES6 default export)
- `export const name = {}` (ES6 named export)

##### Defining imports
`import` and `require` statements are used to import modules
- `const name = require('./{filename}')` (CommonJS way)
- `import name from './{filename.js}'` (ES6 default)
- `import {module} from './{filename.js}'` (ES6 named export, function name inside braces)
- `import fs from 'fs'` (ES6 core module or installed 3rd party module)
- can `console.log` name to see the details of the exports object from that file so you know what can be accessed
## Asynchronous Programming in Node.js

Node.js's non-blocking I/O model is central to its design and performance.
- Most asynchronous operations involve network calls, timing, or file system/database interaction.

### Event Loop

- Central to Node.js's non-blocking I/O model.
- Handles asynchronous operations, delegating tasks and managing event callbacks.

### Native JavaScript Async Features
#### Callbacks

- Traditional method for handling asynchronous operations.
- Functions passed as arguments to be called upon completion of an operation.
- This convention allows other code to run in the meantime.

#### Promises

- An alternative to callbacks for handling asynchronous operations.
- Object representing the eventual completion or failure of an asynchronous operation.
- Allows chaining of asynchronous operations with `.then()`, error handling with `.catch()`, and finalization with `.finally()`.

#### Async/Await

- A syntactic feature for writing asynchronous code in a more readable, synchronous-like manner.
- Use `async` before a function to return a Promise and `await` to pause execution until the Promise resolves.

#### Error Handling

- Crucial in asynchronous programming.
- Use `.catch()` with promises and `try...catch` blocks with async/await.
### Node.js 'async' Module

## Common Node modules
##### fs
Node core filesystem module
###### Methods
Synchronous(blocking) filesystem methods - they all end with `Sync`
- `readFileSync('path/to/file')` - returns a `Buffer` object containing the complete file contents.  Convert `Buffer` objects to strings with `toString()`
- 
Asynchronous(non-blocking)
- `readFile('path/to/file')` 
- `readdir('path/name', function(err, filelist){})` - 
- `fs.writeFile('path/to/file', data, callback)`: Asynchronously writes data to a file. The `callback` gets two arguments `(err, data)`.
- `fs.unlink('path/to/file', callback)`: Asynchronously deletes a file. The `callback` gets one argument `(err)`.
##### http
Node core http module
###### Methods
- `.get()` - can take a url as the first argument and a callback function as the second
	- the signature of this callback is `function (response) {}`
	- `.get()` can be appended with `.on('error', console.error)` to listen for an error that occurs while sending the request.
- `.createServer()` - given a callback function as an argument `(function callback(request, response){})`, returns an HTTP `server` that executes the function each time it receives a request.
	- `server.listen({portNum})` - to start listening to a given port
- `.request(options, callback)`: Sends an HTTP request to a server. `options` can be an object or a string. If `options` is a string, it is automatically parsed with `url.parse()`.
##### net
Node core basic networking module
###### Methods
- `.createServer()` - takes a connection listener function as an argument and returns a server instance
	- Every connection received by the server triggers another call to the listener
	- Listener function signature: `function listener (socket) {}`

 A typical Node TCP server looks like this:  
   
     const net = require('net')  
     const server = net.createServer(function (socket) {  
       // socket handling logic  
     })  
     server.listen(8000)


##### path
For working with file paths
###### Methods
- `path.join([...paths])`: Joins all given path segments together using the platform-specific separator as a delimiter.
- `path.resolve([...paths])`: Resolves a sequence of paths or path segments into an absolute path.
- `path.basename(path[, ext])`: Returns the last portion of a path. Similar to the Unix basename command.
- `path.extname(path)`: Returns the extension of the path, from the last occurrence of the '.' (period) character to end of string in the last portion of the path.

##### os
For retrieving operating system related information
###### Methods
- `os.platform()`: Returns a string identifying the operating system platform.
- `os.cpus()`: Returns an array of objects containing information about each logical CPU core.
- `os.freemem()`: Returns the amount of free system memory in bytes.
- `os.totalmem()`: Returns the total amount of system memory in bytes.

##### async
A rich set of functions for complex and advanced asynchronous operations.
[Official Async Documentation](https://caolan.github.io/async/v3/docs.html)
###### Methods
Control Flow:
- `async.series`
- `async.parallel`
- `async.waterfall`
- `async.whilst`
Collection Functions:
- `async.each([],{})` - Calls an async iterator function on each element of an array that is given as the first argument.
- `async.map` - Like async.each, but collects the results into an array and passes them to the callback.
- `async.filter`
Utility Functions:
- `async.queue`
- `async.retry`

##### crypto
Cryptographic operators
###### Methods
- `crypto.createHash(algorithm)`: Creates and returns a hash object, a cryptographic hash with the given algorithm which can be used to generate hash digests.
- `crypto.randomBytes(size[, callback])`: Generates cryptographically strong pseudo-random data. The `size` argument is a number indicating the number of bytes to generate.
## Links
- [Node.js website](https://nodejs.org/en/)
- [Node Version Manager (NVM)](https://github.com/nvm-sh/nvm)
- [learnyounode program](https://github.com/workshopper/learnyounode)
- [async-you program](https://github.com/bulkan/async-you) for learning the Node 'async' module
- Intro to Node Frontend Masters [resources](https://scottmoss.notion.site/scottmoss/Intro-to-Node-js-V3-7c8e4ccaebf94b839f425fff13dcc44c)
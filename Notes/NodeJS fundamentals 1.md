Requirements : [[02 - Coding/Backend/Backend fundamentals]]

---

# Introduction %% fold %%

- ✅**Node.js** is an open-source cross-platform JavaScript **runtime environment**.
- ❌ **Node.js** is **not a framework**.

- **Node.js** was created by **_Ryan Dahl_** in **2009**.
- **Node.js** runs the google chrome's **V8 JavaScript engine** outside of the browser.

- Node.js apps run in a **single process**, without creating a new thread for every request.
- Node.js uses **ECMAScript** standards for compatibility.

> [!success]+ Node JS functioning
> **Node.js** uses an **single-threaded**, **event-driven** & **asynchronous I/O model**, efficient for building scalable real-time apps and web servers.
>
> ##### **Single threaded**:
>
> -   A **thread** is a **sequence of instructions** that a program follows.
> -   Because the Node.js consists of a **single thread**, it can only do one thing at a time.
>
> ##### **Event-driven**:
>
> -   Node.js is always **listening for events** things to happen.
> -   When something happens, it triggers a response or action.
>
> ##### **Asynchronous I/O (Non-blocking I/O)**:
>
> -   Normally, programs wait for tasks to finish before moving on.
> -   Node.js generally keeps working on other tasks while waiting for results.

---

# Node Package Manger (`npm`) %% fold %%

**npm** (Node Package Manager) is the default **package manager** for **Node.js**.

- `node_modules`folder holds all the project’s **packages(_dependencies_)**.
- `package.json` file holds **info(_metadata_)** about the installed dependencies.
- `package-lock.json` file **locks the exact versions** of all dependencies & ensures consistent installs across different environments.

## npm commands %% fold %%

### 1. Initializing New Project

- To start a new Node.js project, create a `package.json` file:

```bash
npm init
```

(Use `npm init -y` to skip prompts and auto-generate `package.json`.)

### 2. Installing Dependencies

1. To install all dependencies listed in `package.json`:

```bash
npm install
```

2.  To install a specific package:

```bash
npm install <package-name>
```

3.  To install a package as a development dependency:

```bash
npm install --save-dev <package-name>
```

### 3. Uninstalling Dependencies

- To remove a specific package from your project:

```bash
npm uninstall <package-name>
```

### 4. Running Scripts

- Run defined scripts in `package.json`:

```bash
npm run <script-name>
```

### 5. Updating Packages

- To update all installed packages to the latest versions:

```bash
npm update
```

### 6. Checking for Vulnerabilities

- To check for known security vulnerabilities within dependencies.

```bash
npm audit
```

---

## How npm Works %% fold %%

### 1. Installing Packages

When you install a package (`npm install <package-name>`):

- npm downloads the package from the npm registry.
- Adds it to your `node_modules` folder.
- Updates the `package.json` file to include it as a dependency.
- Creates/updates the `package-lock.json` file to ensure exact versions are used.

### 2. Versioning in npm

- npm uses **semantic versioning** (`semver`) to determine compatible versions of packages.

- Show node version:

```bash
node --version
```

- **Major version** (`1.x.x`): Introduces breaking changes.
- **Minor version** (`x.1.x`): Adds new features in a backward-compatible way.
- **Patch version** (`x.x.1`): Fixes bugs in a backward-compatible way.

```json
"dependencies": {
	"express": "^4.17.1"
}
// ^ Will install any version >=4.17.1 <5.0.0
```

### 3. Global vs Local Packages

- **Local Installation**: Installs packages into the `node_modules` folder of the current project (typically used for dependencies).

```bash
npm install <package-name>
```

- **Global Installation**: Installs packages globally on your system, making them available to all projects ( used for CLI tools like `eslint`, `nodemon`).

```bash
npm install -g <package-name>
```

### 4. Other npm tools

#### npx

- A tool bundled with npm (v5.2 onwards) that allows you to
    **run executable packages without installing them globally**.

```bash
npx create-react-app my-app
```

This will run the `create-react-app` package without installing it globally.

#### npm ci

- A faster, cleaner alternative to `npm install`.
- Ensures a **clean install** by deleting the `node_modules` folder & installing exactly what's listed in `package-lock.json`.
- Ideal for CI/CD pipelines.

```bash
npm ci
```

#### nvm

- `nvm` allows you to quickly **install and use different versions** of node via the command line.

```bash
nvm use 16
```

---

# Hello World in Node.js %% fold %%

```js
// Import the `createServer` function from Node's built-in `http` module
import { createServer } from "node:http";

// Define the server's hostname (localhost - your own computer)
const hostname = "localhost";

// Define the port number the server will listen on
const port = 5000;

// Create server as a function using `createServer()`
// Arguments of `createServer()` : (`req`: request) & (`res`: response)
const server = createServer((req, res) => {
	// response: status code = 200 (OK)
	res.statusCode = 200; // response: header = plain text

	res.setHeader("Content-Type", "text/plain"); // response: end = 'Hello World'

	res.end("Hello World");
});

// Start server and listen on the given `hostname` and `port`
server.listen(port, hostname, () => {
	// While the server is running, log message in the console
	console.log(`Server running at http://${hostname}:${port}/`);
});
```

To run this, save as `server.mjs` & run in terminal:

```bash
node server.mjs
```

---

> [!tip]+ Tip: Use Nodemon package
> It **automatically restarts the server** whenever changes are made in the files.
>
> ##### Installation
>
> Local install:
>
> ```bash
> npm install --save-dev nodemon
> ```
>
> Global install:
>
> ```bash
> npm install --g nodemon
> ```
>
> > [!info]+ --save-dev
> > It will add the package to the **`devDependencies`** section rather than `dependencies` section of `package.json`.
> >
> > -   `dependencies`: Packages needed to run project in **production**.
> > -   `devDependencies`: Packages **only needed during development**.

> [!info]+ CJS & MJS
>
> # CJS (_Common JavaScript_)
>
> -   **Common JavaScript** is a module system used in ~={green}**Node.js**=~ for **only server-side** applications.
> -   Uses `.cjs` extension.
> -   Import : `const moduleName = require('module-path');`
> -   Export : `module.exports.<functionName> = <value>;`
>
> ---
>
> # MJS (**ES Modules**) (_Module JavaScript_)
>
> -   **Module JavaScript** (ES Modules) is a module system used in ~={yellow}**browsers**=~ & ~={green}**Node.js**=~ (from version 12 onwards), for **client-side** & **server-side** applications.
> -   Import : `import <moduleName> from 'module-path';`
> -   Export : `export <value> from 'module-path';`

---

# Global variables %% fold %%

- In Node.js, **global variables** are those variables that are accessible throughout the application (without needing any `imports` or `require` statements.).
- These are provided by Node.js and are **automatically available** without having to import or define them.

---

### 1. Global Variables in Node.js %% fold %%

- Built-in values automatically available in every module.
- Provide information about the environment and current module.

| **Name**        | **Description**                                                                 | **Example**                                                               |
| --------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `__dirname`     | Absolute path of directory containing current module.                           | `console.log(__dirname);`<br>Output: `/path/to/project`                   |
| `__filename`    | Absolute path of currently executing file.                                      | `console.log(__filename);`<br>Output: `/path/to/project/app.js`           |
| `module`        | Represents current module, provides access to its functions & metadata.         | `console.log(module);`<br>Outputs module details                          |
| `exports`       | A shorthand for `module.exports`, used to export functions from a module.       | `exports.sayHello = function() { console.log('Hello!'); };`               |
| `require()`     | Used to import modules into current script.                                     | `const fs = require('fs');`                                               |
| `console`       | Provides methods for outputting to the console.                                 | `console.log('Hello, world!');`                                           |
| `setTimeout()`  | Schedules a function to **run once** after a delay<br>(in milliseconds).        | `setTimeout(() => { console.log("Hello after 2 seconds"); }, 2000);`      |
| `setInterval()` | Schedules a function to **run repeatedly** at an interval<br>(in milliseconds). | `setInterval(() => { console.log("This runs every 3 seconds"); }, 3000);` |

---

### 2. Global Objects in Node.js %% fold %%

- Objects and functions available throughout the application.
- Allow interaction with system resources and process management.

| **Name**          | **Description**                                                                     | **Example**                                                                                               |
| ----------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `global`          | Represents global scope. Variables added to `global` object are available globally. | `global.myVar = 'I am global'; console.log(myVar);` <br>Output: `I am global`                             |
| `process`         | Provides info about current process.                                                | `console.log(process.pid);` <br>Output: Process ID                                                        |
| `Buffer`          | Used for working with raw binary data directly.                                     | `const buf = Buffer.from('Hello'); console.log(buf.toString());` <br>Output: `Hello`                      |
| `setTimeout()`    | Schedules a function to **run once** after a delay<br>(in milliseconds).            | `setTimeout(() => { console.log('Executed after 2s'); }, 2000);`                                          |
| `clearTimeout()`  | Clears a previously set timeout.                                                    | `const id = setTimeout(() => { console.log("Not this"); }, 5000); clearTimeout(id);`                      |
| `setInterval()`   | Schedules a function to **run repeatedly** at an interval<br>(in milliseconds).     | `setInterval(() => { console.log('Repeated every 3 seconds'); }, 3000);`                                  |
| `clearInterval()` | Clears a previously set interval.                                                   | `const interval = setInterval(() => { console.log("Not this either"); }, 1000); clearInterval(interval);` |

---

# FS Module %% fold %%

- The **File System Module** or `fs` module in Node.js provides a set of methods for interacting with the **file system**.
- It allows both **synchronous** and **asynchronous** operations like reading, writing, updating, and deleting files and directories.

## Common methods in `fs` module

| Async Method               | Sync Alternative      | Description                              |
| -------------------------- | --------------------- | ---------------------------------------- |
| `fs.readFile()`            | `fs.readFileSync()`   | Reads a file asynchronously              |
| `fs.writeFile()`           | `fs.writeFileSync()`  | Writes to a file (creates if not exists) |
| `fs.appendFile()`          | `fs.appendFileSync()` | Appends data to a file                   |
| `fs.rename()`              | `fs.renameSync()`     | Renames a file                           |
| `fs.unlink()`              | `fs.unlinkSync()`     | Deletes a file                           |
| `fs.mkdir()`               | `fs.mkdirSync()`      | Creates a new directory                  |
| `fs.readdir()`             | `fs.readdirSync()`    | Reads the contents of a directory        |
| `fs.stat()`                | `fs.statSync()`       | Gets metadata                            |
| `fs.promises.access()`<br> | `fs.existsSync()`     | Checks if a file exists                  |

---

# Promises %% fold %%

- A **Promise** is an _object that represents the eventual completion_ (or failure) of an asynchronous operation and its resulting value.
- It allows **asynchronous** code to be written in a more readable, manageable, and maintainable way.

## States of a Promise %% fold %%

| State         | Description                                                         |
| ------------- | ------------------------------------------------------------------- |
| **Pending**   | The initial state, before the operation is completed.               |
| **Fulfilled** | The operation was successful, and the Promise has a resolved value. |
| **Rejected**  | The operation failed, and the Promise has an error or reason.       |

---

## Creating a Promise %% fold %%

```js
const myPromise = new Promise((resolve, reject) => {
	let success = true;
	if (success) {
		resolve("Operation was successful");
	} else {
		reject("Operation failed");
	}
});
```

The constructor accepts an **executor function**, which contains the asynchronous logic.

- **resolve()**: Called when the operation is successful (fulfills the promise).
- **reject()**: Called when the operation fails (rejects the promise).

---

## Handling Promises %% fold %%

```js
myPromise
	.then((result) => console.log(result)) // Handles fulfillment
	.catch((error) => console.log(error)) // Handles rejection
	.finally(() => console.log("Promise settled"));
```

- **`then()`**: Handles the fulfilled value of a Promise.
- **`catch()`**: Handles errors when a Promise is rejected.
- **`finally()`**: Executes code after the Promise settles (whether fulfilled or rejected).

---

## Promise Chaining %% fold %%

- Promises support **method chaining** using `.then()` for sequential handling.
- **Each `.then()` returns a new Promise**, so you can chain multiple operations.

```js
myPromise
	.then((result) => {
		console.log(result);
		return "Next step"; // Returning a new value
	})
	.then((nextResult) => console.log(nextResult)); // Chain another then()
```

---

## Promise Methods %% fold %%

JavaScript provides several **static methods** on the `Promise` object to handle multiple Promises.

### 1. **`Promise.all()`**:

- Waits for all Promises in an array to resolve.
- If one Promise rejects, the entire operation fails.
- Returns an array of results from all resolved Promises.

**Example**:

```js
Promise.all([promise1, promise2, promise3])
	.then((results) => console.log(results))
	.catch((error) => console.log("One of the promises failed"));
```

---

### 2. **`Promise.allSettled()`**:

- Waits for all Promises to settle, regardless of whether they are resolved or rejected.
- Returns an array of objects with the status (`"fulfilled"` or `"rejected"`) and value/reason for each Promise.

**Example**:

```js
Promise.allSettled([promise1, promise2, promise3]).then((results) =>
	console.log(results)
);
```

---

### 3. **`Promise.race()`**:

- Returns the result of the **first** resolved or rejected Promise.
- Useful for timeouts or the "first to finish" scenario.

**Example**:

```js
Promise.race([promise1, promise2])
	.then((result) => console.log(result))
	.catch((error) => console.log(error));
```

---

### 4. **`Promise.any()`**:

- Returns the **first Promise** that resolves.
- If all Promises reject, it throws an `AggregateError`.

**Example**:

```js
Promise.any([promise1, promise2])
	.then((result) => console.log(result))
	.catch((error) => console.log("All promises rejected:", error));
```

---

## Async/Await %% fold %%

- **`async`/`await`** provides a more synchronous-like way to work with Promises.
- An **`async` function** always returns a **Promise** (accepted or rejected).
- The **`await`** keyword pauses the execution of the `async` function until the Promise is resolved or rejected.

### 1. `async` Function

- An `async` function **always returns a Promise** (accepted or rejected).
- When an `async` function returns a value, it will **always wrap the value with Promise**.
- When an `async` function throws an error, **it always returns a rejected Promise**.

### 2. `await` Keyword

- **`await`** is used **inside** an `async` function and it can only be used within an `async` context.
- **`await`** pauses the execution of the `async` function until the **Promise** it is waiting on resolves or rejects.
- The value of the **resolved Promise** is returned when the `await` expression completes.

```js
async function fetchData() {
	try {
		const response = await fetch("https://api.example.com");
		const data = await response.json();
		console.log(data);
	} catch (error) {
		console.log("Error:", error);
	}
}

fetchData();
```

> [!warning]+ Warning
>
> -   **Unhandled Promise Rejections**: If a Promise is rejected and the rejection is not handled with `.catch()`, it can lead to unhandled errors and bugs.
> -   **Chaining Breaks**: Promises are resolved or rejected once. Skipping or breaking chains by returning values prematurely can cause problems.
> -   **Nested Promises**: To prevent nested promises use `async/await` to flatten the structure.

---

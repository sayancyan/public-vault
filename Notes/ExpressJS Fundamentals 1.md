Requirements: [[02 - Coding/Backend/Backend fundamentals]] ,[[NodeJS fundamentals]]

# Introduction %% fold %%

**ExpressJS** is a minimal and flexible server-side **Node.js framework** that is used to create APIs & develop web apps.

## Features of ExpressJS %% fold %%

- **Routing**: Defines URL paths & handles HTTP methods.
- **Middleware**: Functions that handle requests and responses.
- **Template Engines**: Supports rendering of dynamic HTML. (Pug, EJS).
- **Static Files**: Serves static assets like images, CSS, and JS.
- **Error Handling**: Built-in mechanism for handling errors.

---

# Installation %% fold %%

## Step 1: Create project directory %% fold %%

Create a project directory and go to the directory.

```bash
mkdir myapp
cd myapp
```

## Step 2: Initialise Node %% fold %%

Use `npm init` command to create a `package.json` file for your application.

```bash
npm init -y
```

## Step 3: Install Express %% fold %%

Below code, installs **Express** in the directory & saves it in the dependencies list.

```bash
npm install express
```

---

# Routing %% fold %%

- **Routing** refers to defining ~={yellow}how an application responds=~ to ~={yellow}client requests=~ at a ~={yellow}specific endpoints=~.
- Endpoints are determined by **URI (Uniform Resource Identifier)** and a specific **HTTP request method**.
- Each route is associated with a **callback function** that executes when the route is matched.

---

## Callback Function %% fold %%

- A **callback function** is a function that is **passed as an argument to another function**.
- It is executed **after the parent function** completes.
- In the context of **ExpressJS**, callback functions are used to **handle HTTP requests**.
- In ExpressJS Routing, the callback function is executed **when a request matches the route**.

> [!example]+ Example
>
> ```js
> app.get("/", function (req, res) {
> 	res.send("Hello World");
> });
> ```
>
> -   `function (req, res)` is the **callback function**.
> -   It gets called when a GET request is made to `/`.

> [!info]+ Arguments of Callback function
>
> -   `req` → Request object (contains details of the request).
> -   `res` → Response object (used to send data back to the client).
> -   `next` _(optional)_ → Function used to pass control to the next middleware.

> [!bug]+ Callback Hell
> **Callback Hell** is a term used in **asynchronous programming** to describe a situation where multiple **nested callbacks** make code difficult to read, maintain, and debug.
>
> > [!example]+ Example
> >
> > ```js
> > getUser(userId, (user) => {
> > 	getPosts(user.id, (posts) => {
> > 		getComments(posts[0].id, (comments) => {
> > 			updateUI(comments, () => {
> > 				console.log("UI updated");
> > 			});
> > 		});
> > 	});
> > });
> > ```

> [!success] Solution to Callback Hell
>
> 1. Modularize the Code using named functions.
> 2. Use Promises module.
> 3. Use async and await functions.

---

## Basic Route Structure %% fold %%

The general syntax structure for defining a **route** in ExpressJS is:​

```syntax
app.method(path, handler)
```

Where:

- **app**: Variable holding an _instance of Express_ (express app).
- **method**: HTTP method in lowercase (e.g., `get`, `post`, `put`, `delete`).​
- **path**: Server path (endpoint).​
- **handler**: Function executed when the route is matched.

### Example

```js
// Import the Express module using ES module syntax (mjs)
import express from "express";

// Create a variable 'app' and stores an instance of the Express app
const app = express();

//----------------------------------------------------------
// Routes

// Respond with `Hello World!` on the homepage:
app.get("/", (req, res) => {
	res.send("Hello World!");
});

// Respond to POST request on the root route/homepage (`/`):
app.post("/", (req, res) => {
	res.send("Got a POST request");
});

// Respond to a PUT request to the `/user` route:
app.put("/user", (req, res) => {
	res.send("Got a PUT request at /user");
});

// Respond to a DELETE request to the `/user` route:
app.delete("/user", (req, res) => {
	res.send("Got a DELETE request at /user");
});

//----------------------------------------------------------

// Start the server (optional but typical)
app.listen(3000, () => {
	console.log("Server is running on http://localhost:3000");
});
```

---

## Parameters %% fold %%

### 1. Route Parameters %% fold %%

- **Route parameters** are **dynamic segments in a URL** that act like variables.
- Used in Express.js to **capture values directly from the URL path**.
- Defined using `:` in the route.
- Accessed via: `req.params.id`

> [!example]+ Example
>
> ```js
> app.get("/user/:id", (req, res) => {
> 	const userId = req.params.id;
> 	res.send(`User ID is: ${userId}`);
> });
> ```
>
> -   If someone visits `/user/42`, this will respond with:
>
> ```pgsql
> User ID is: 42
> ```

> [!info]+ Anatomy of a Route Parameter
>
> `/user/:id`
>
> -   `:id` is a **route parameter**.
> -   It will match anything in that spot of the URL.
> -   The value is available in `req.params.id`.

---

### 2. Query Parameters %% fold %%

- **Query parameters** are used to send additional data in the URL after the `?` symbol.
- They are typically used to **filter or customize the request**.
- They are appended to the base URL after the `?` symbol.
- Expressed in the format `key=value`, separated by `&`.
- Accessed via: `req.query.<parameter>`

> [!example]+ Example
>
> ```js
> app.get("/search", (req, res) => {
> 	const searchTerm = req.query.term;
> 	res.send(`Search results for: ${searchTerm}`);
> });
> ```
>
> -   If someone visits `/search?term=express`, this will respond with:
>
> ```pgsql
> Search results for: express
> ```

> [!info]+ Anatomy of a Query Parameter
>
> `/search?term=express&limit=10`
>
> -   `term=express` is a **query parameter**.
> -   `limit=10` is another **query parameter**.
> -   Both values are available via `req.query.term` and `req.query.limit`.

---

---

## Working of Routes %% fold %%

A simple app that has 3 pages **root**, **home** & **about**.

```Folder_Structure
/project
│
├── /routes
│   ├── root.mjs
│   ├── home.mjs
│   └── about.mjs
│
├── main.mjs
└── package.json
```

---

> [!success]- main.mjs
>
> ```js
> import express from "express";
>
> // importing routes
> import root from "./routes/root.mjs";
> import home from "./routes/home.mjs";
> import about from "./routes/about.mjs";
>
> const app = express();
> const port = 3000;
>
> //middlewares
> app.use(express.static("public"));
>
> app.use("/", root);
> app.use("/home", home);
> app.use("/about", about);
>
> app.listen(port, () => {
> 	console.log(`Server Started...\nListening at PORT: ${port}`);
> });
> ```

> [!success]- `/` route
>
> ```js
> import express from "express";
> const router = express.Router();
>
> router.get("/", (req, res) => {
> 	console.log(`Endpoint: ${req.originalUrl}`);
> 	res.send(`Endpoint: ${req.originalUrl}`);
> });
>
> export default router;
> ```

> [!success]- `/home` route
>
> ```js
> import express from "express";
> const router = express.Router();
>
> router.get("/home", (req, res) => {
> 	console.log(`Endpoint: ${req.originalUrl}`);
> 	res.send(`Endpoint: ${req.originalUrl}`);
> });
>
> export default router;
> ```

> [!success]- `/about` route
>
> ```js
> import express from "express";
> const router = express.Router();
>
> router.get("/about", (req, res) => {
> 	console.log(`Endpoint: ${req.originalUrl}`);
> 	res.send(`Endpoint: ${req.originalUrl}`);
> });
>
> export default router;
> ```

> [!info]- Note
>
> ```js
> Endpoint: ${req.originalUrl}
> ```
>
> -   `$req.originalUrl` gives the current route URL.

---

## Middleware %% fold %%

- **Middleware functions** can access the **request (`req`) and response (`res`)** objects.
- They also receive a **`next` function**, which passes control to the next middleware in the stack.

- Tasks performed by middleware functions:
    - Executes code.
    - Update request(`req`) & response(`res`) objects.
    - End(`end`) the request-response cycle.
    - Call the next(`next`) middleware function in the stack.

### `app.use()` %% fold %%

- `app.use()` is a method used to **mount middleware functions** or **routes** onto the Express application.
- This tells Express: “For **every** incoming request, run this middleware.”

```js
app.use((req,res,next) => {
	console.log('Midddelware')
	next()
})

//-----------------------------------

// Or, if using routes :
import <router> from '/path'
app.use(<router>)


```

> [!example]+ Common Uses of `app.use()`
>
> 1. Serving Static Files
>     - Serve static files like HTML, CSS, JS, images, etc.
>
> ```js
> app.use(express.static("public"));
> ```
>
> 2. Mounting Routers
>
>     - Mount a router on a specific path.
>
> ```js
> import userRouter from ("./routes/users");
> app.use("/users", userRouter);
> // All routes inside userRouter will be prefixed with /users
> ```

### Types of middleware %% fold %%

- [Application-level middleware](https://expressjs.com/en/guide/using-middleware.html#middleware.application)
- [Router-level middleware](https://expressjs.com/en/guide/using-middleware.html#middleware.router)
- [Error-handling middleware](https://expressjs.com/en/guide/using-middleware.html#middleware.error-handling)
- [Built-in middleware](https://expressjs.com/en/guide/using-middleware.html#middleware.built-in)
- [Third-party middleware](https://expressjs.com/en/guide/using-middleware.html#middleware.third-party)

---

1. **`main.mjs`**: This file serves as the **entry point** to the application.

    - It imports route files from `/routes` & associates them with URL endpoints.
    - The `app.use` method **handles requests** for specific paths with the corresponding route handlers.

2. **Routing Logic**:
    - **`app.use('/', root)`**:
      Routes all requests that hit `/` to `root.mjs` file.
    - **`app.use('/home', home)`**:
      Routes all requests that hit `/home` to `home.mjs` file.
    - **`app.use('/about', about)`**:
      Route all requests that hit `/about` to `about.mjs` file.

---

# Static Files %% fold %%

**Static files** are files that **do not change dynamically** and are sent to the client's browser **as-is**.

- Examples:
    - HTML files
    - CSS stylesheets
    - JavaScript scripts
    - Images (JPG, PNG, SVG)
    - Fonts

## Serving Static Filles %% fold %%

1. Create a folder (e.g. `public`) and put your static files inside it.
2. Folder Structure Example:

```sql
project/
│
├── public/
│   ├── index.html
│   ├── style.css
│   └── script.js
│
└── app.js

```

3. Use the built-in middleware `express.static()` to serve static files in public folder.

```js
app.use(express.static("public"));
```

---

# Slugs in Express %% fold %%

- A **slug** is a **simplified string** derived from a resource’s title or name.
- It is used to represent a specific resource in a readable format.
- It is **SEO-friendly** (Search Engine Optimization).

```http
https://example.com/blog/understanding-express-routing
```

- `understanding-express-routing` is the slug.

## Installing Slug %% fold %%

```bash
npm install slugify
```

## Using Slugs %% fold %%

```js
import slugify from "slugify";

const title = "ExpressJS Fundamentals & Routing";
const slug = slugify(title, { lower: true });

console.log(slug); // Output: expressjs-fundamentals-routing
```

```output
expressjs-fundamentals-routing
```

## Handling Slugs in ExpressJS %% fold %%

- Slugs are handled using **route parameters** in ExpressJS.
- `:slug` is a **dynamic parameter**.

```js
app.get("/blog/:slug", (req, res) => {
	const slug = req.params.slug;
	// Logic to find and serve the content based on the slug
	res.send(`Blog post for slug: ${slug}`);
});
```

- `:slug` tells Express to take _anything_ written in this part of the URL & treat it as a variable called `slug`.
- `req.params.slug` retrieves the slug from the URL.
- Slugs can then be used to get **specific data** from database.

---

## Slug advantages %% fold %%

- 📌 **Readability**: Clear URLs are user-friendly.
- 🔍 **SEO**: Search engines rank descriptive URLs better.
- 🧩 **Identifiability**: Easy to remember and identify resources.
- 🛡️ **Avoids Exposure of IDs**: Hides sensitive internal IDs from public view.

---

# Template Engine (EJS) %% fold %%

- **Template engine** is a tool used to **render dynamic content** on the server side.
- **EJS (Embedded JavaScript)** is a simple **templating language**.
- It helps to **generate HTML markup** with plain **JavaScript**.

> [!tip] EJS documentation for Express:
>
> https://github.com/mde/ejs/wiki/Using-EJS-with-Express

---

| **Function**   | **Description**                                          | **Example**                                                                                                         |
| -------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `app.get()`    | Handles GET requests.                                    | `app.get('/path', (req, res) => { res.send('Response'); });`                                                        |
| `app.post()`   | Handles POST requests.                                   | `app.post('/path', (req, res) => { res.send('Data received'); });`                                                  |
| `app.put()`    | Handles PUT requests.                                    | `app.put('/path', (req, res) => { res.send('Data updated'); });`                                                    |
| `app.delete()` | Handles DELETE requests.                                 | `app.delete('/path', (req, res) => { res.send('Resource deleted'); });`                                             |
| `app.listen()` | Listens for connections on a specified port.             | `app.listen(3000, () => { console.log('Server is running'); });`                                                    |
| `app.use()`    | Registers middleware globally or for specific routes.    | `app.use(express.json());`                                                                                          |
| `app.route()`  | Chains multiple HTTP method handlers for the same route. | `app.route('/user') .get((req, res) => { res.send('GET user'); }) .post((req, res) => { res.send('POST user'); });` |

---

| **Function** | **Description**                                             | **Example**                                                         |
| ------------ | ----------------------------------------------------------- | ------------------------------------------------------------------- |
| `req.params` | Retrieves route parameters from the URL (dynamic segments). | `app.get('/user/:id', (req, res) => { res.send(req.params.id); });` |
| `req.query`  | Retrieves query string parameters from the URL.             | `app.get('/search', (req, res) => { res.send(req.query.term); });`  |
| `req.body`   | Retrieves the body of the request.                          | `app.post('/submit', (req, res) => { res.send(req.body.data); });`  |

---

| **Function**     | **Description**                                               | **Example**                                  |
| ---------------- | ------------------------------------------------------------- | -------------------------------------------- |
| `res.send()`     | Sends a response to the client, can send text, HTML, or JSON. | `res.send('Response Text');`                 |
| `res.json()`     | Sends a JSON response.                                        | `res.json({ message: 'Success' });`          |
| `res.status()`   | Sets the HTTP status code for the response.                   | `res.status(404).send('Not Found');`         |
| `res.redirect()` | Redirects the client to a different URL.                      | `res.redirect('/new-url');`                  |
| `res.sendFile()` | Sends a file as a response (typically used for static files). | `res.sendFile('/path/to/file.html');`        |
| `res.render()`   | Renders a view using a template engine (e.g., EJS).           | `res.render('index', { title: 'Express' });` |

| **Function**           | **Description**                                                        | **Example**                                        |
| ---------------------- | ---------------------------------------------------------------------- | -------------------------------------------------- |
| `express()`            | Creates an Express application instance.                               | `const app = express();`                           |
| `express.json()`       | Middleware to parse JSON data in the request body.                     | `app.use(express.json());`                         |
| `express.urlencoded()` | Middleware to parse URL-encoded data (e.g., from forms).               | `app.use(express.urlencoded({ extended: true }));` |
| `express.static()`     | Serves static files such as images, stylesheets, and JavaScript files. | `app.use(express.static('public'));`               |

---

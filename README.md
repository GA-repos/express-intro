[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)


<br>
<img src="https://i.imgur.com/vUOu9NW.jpg">
<br>


# Intro to Express

Today is a big day in SEI! We've build front-end applications using our knowledge and expertise of HTML, CSS and JavaScript. Over the next few weeks we're going to venture in to new territory: building full-stack applications!

The framework we'll be using in this unit is called ExpressJS (Express). Express runs on NodeJS and provides us with some help in building out fullstack applications and APIs.

## Objectives

By the end of this lesson, developers should be able to:

- Explain and understand the request-response cycle
- Discuss how the Web works including:
  - Browser requests
  - Status codes
  - HTTP methods and REST
- Build a simple server-side application with Express

## Introduction

Express is a framework for building web applications. In software development, frameworks include support programs, compilers, code libraries, tool sets, and application programming interfaces (APIs) that bring together all the different components to enable development of a project or system. There are lots of different kinds of frameworks for different kinds of tasks.  Express helps us build applications on NodeJS for the World Wide Web (Web).

## How does the Web Work

Before we can build our first full-stack application, we need to discuss how the Web works. Once we know a little bit about how the Web works, we can start to think about how Express (our back-end) fits in with our front-end.

### Client-Server

The Web follows a model of communication called `client-server`. In the context of the Web, our browsers serve as the `client`. The other side of the equation is the `server` - a computer or application somewhere that responds to the requests from our browser.

![Client-Server](https://media.git.generalassemb.ly/user/17300/files/8d5a2c80-4670-11ea-8a29-610723d36c34)

The client and server communicate using Hypertext Transfer Protocol (HTTP) and the `request-response` cycle.

<img src="https://i.imgur.com/clxiqnO.png" style="width:80%">

### HTTP

HTTP is a **protocol** which establishes the rules for communication over the Web. HTTP dictates how the client requests information from a server and how the server responds. Each message is similarly formatted - so you can think of them as like electronic telegrams.

The process of a client sending a HTTP request, and server responding is known as the **HTTP Request/Response Cycle**:

	<img src="https://i.imgur.com/Iqsj9gF.png" style="width:80%">

Requests always have these three parts:

1. Request line (including the URL and the HTTP Method)
1. Request header (additional information about the request and what we expect in the response)
1. Body message (optional - things like form data)

Responses in turn always have these three parts:

1. Status (a status code indicating how the request was handled)
1. Response header (additional information about the response)
1. Body message (optional - an html document, JSON, XML)


When we browse to a website by typing in the address bar, this is what happens:

	<img src="https://i.imgur.com/JDFHoZl.png" style="width:80%">


Clients make requests to a location (called a URL) using a method.

<img width="1569" alt="url" src="https://media.git.generalassemb.ly/user/17300/files/63086f00-4670-11ea-94be-9ba3acdb30f1">

There are 10 possible HTTP methods, but the 5 that we'll be focused on are:

| Method Name | Description |
| --- | --- |
| GET | Used for retrieving data from a server. |
| POST | Used for sending data to the server. |
| PUT | Used for replacing data on the server. |
| PATCH | Used for updating data on the server. |
| DELETE | Used for deleting data from the server. |

When the server receives a request, it processes the message and then sends a response. The server always sends a response, though sometimes that response is just to tell the client that there was an error.

The status codes are also defined by the protocol:

| Status Code | Description | Example
| --- | --- | --- |
| 1xx | Informational | 101 Continue |
| 2xx | OK | 201 Created |
| 3xx | Redirection | 301 Moved Permanently |
| 4xx | Client Errors | 404 Not Found |
| 5xx | Server Errors | 500 Internal Server Error |


<img src="https://i.imgur.com/fuED3VM.png" style="width:80%">

#### How does it actually work

When you type a URL in the navigation bar of your browser, you make a GET request to that URL (i.e. `http://www.google.com`). The server receives that message and formulates a response: a 200 status code (to indicate everything worked out just fine) and an HTML document for the Google home page.

When you click on a link, you're making a GET request to a URL, just like when you type the URL in the navigation bar of your browser. The server receives the request and sends a response with a new HTML document for you.

When you submit a form, you make a POST request.  Data from the form is sent as part of the request body. The server processes the request (perhaps saving the request body to a database) and then sends a response.

### Modern Web Applications

When the Web was first created, you would request a document that already existed on the server. So when you typed in `http://www.timberners-lee.com`, you received an HTML document on Tim's server. If you wanted to see the about page on Tim's website, you would navigate to `http://www.timberners-lee.com/about.html`. The important thing to note is that someone wrote those HTML pages in full and by hand.

That worked well when the Web was just used for sharing scientific documents, but imagine how different the web would be if you had to create and maintain a separate HTML document for every page in your web app! What a load of work! We don't have time for that! We're programmers!

> True story: this is why PHP was created.

Instead of writing all that HTML by hand, we send data to the client or dynamically generate an HTML document from a template and send that document using Express and other web frameworks!

## Express

Express is a minimalistic web framework. Compared to web frameworks like Django and Ruby on Rails, Express is tiny. It was intentionally designed that way. It's both minimal and unopinionated.  This minimalism comes with some trade-offs. On the one hand, you it's extremely flexible and doesn't unnecessarily bloat your code with things that you don't need. It also means you'll be responsible for building out everything you do need.

At it's core, Express is meant to be a very light abstraction over the native Node HTTP modules as a way of giving developers a few convenient features:

- Routing
- Views
- Middleware
- Modularity with subapplications

These are the core features of Express.

## Setting up an Express App

1. Create a new directory called "express-hello-world" in your sandbox.
1. Change into the new directory
1. Run `npm init -y`.
1. Type `npm install express` or the shorthand version of `npm i express`.
1. Work through the rest of this lesson

### Getting Started

Building our first server is pretty straightforward. Create an `index.js` file and write the following inside of it:

```js
const express = require("express")
const app = express()

app.listen(4000, () => {
  console.log("app listening on port 4000")
})
```

To start up our server, we just need to execute this file with node:

```sh
node index.js
```

What's going on here?

- we're requiring the Express module, which is a function that returns an instance of a web app
- we're invoking the module, instantiating a constant app which holds all the methods and state we use to write and run our web app
- we're starting our server (and app) by listening on port 4000 for incoming requests

When we run the application from the terminal, `node index.js`, we can see app listening on port 4000 printed to the terminal. The process continues to run, occupying the shell until we hit ctrl + c.

If we visit `http://localhost:4000` in the browser, we'll see something like this:

```sh
Cannot GET /
```

Our app is running and we're able to visit it in the browser. But we're missing routes!

### Routing

The first key feature that Express provides is simple and easy routing.

A *route* is a URI (path) and an HTTP method. The path is part of the URL, so if we visit `http://www.cat-astrophy.com/whiskers` the URI will be `/whiskers`. The HTTP method will be the method we want to accept: `GET`, `POST`, `PUT`, or `DELETE`.

Express contains a function for each HTTP method which in turn accepts a path as the first argument then some number of callback functions. We'll start with just one callback function.

Let's update `index.js`. Add this above `app.listen()`

```js
app.get('/', (request, response) => {
  response.send('Hello World')
})
```

Let's break down the syntax here.

```js
  app.get()
```

`app` is the variable we've declared above. It's an `instance` of the express server. `get()` is a function that tells express what `http method` to listen for.

```js
  app.get('/')
```

The first argument that `get()` takes is the `path`. This one is set to the root of wherever our server is listening (which is `http://localhost:4000`).

```js
app.get('/', (request, response) => {})
```

The second argument that `get()` takes is a function. It's how we tell express what we want to do when the server receives a GET request at the root `'/'` url. The preferred syntax is to use arrow functions here, to keep it concise.

In the example above, the callback function is given two arguments: the first represents the HTTP request object and the second represents the HTTP response object.

**We always have to send a response**. We do that by using the response variable that we've declared in the callback. So we end up with a working route!

```js
app.get('/', (request, response) => {
  response.send('Hello World')
})
```

We've added a route and a handler for requests to the `'/'` route. In this case, we're sending the string `'Hello World'` as the response. Let's see if this takes effect in the browser:

```
Cannot GET /
```

No change. The running server won't change until we restart it and refresh the page. Once we do that, we'll see:

```
Hello World
```

Constantly needing to restart the server will get very tedious, very quickly. Instead, we can use the `nodemon` module to run our server. Instead of requiring `nodemon` in our code, we use `nodemon` from the command line. Then, `nodemon` will restart our server for us whenever a file is changed.

Install the nodemon package with `npm i nodemon --save`, or with the shorthand `npm i nodemon --D`.  The `--save` or `-D` will install nodemon as a **devDependency** in our `package.json`. That means it will only be used during development, not during production deployments. 

> You can install nodemon globally if you do not have it with `npm install --global nodemon`
>
> When using the `--global` flag (or `-g` for short), we're specifying that `nodemon` will be installed "globally" so we can utilize `nodemon` across all of our node applications (and also that it is not included in our project dependencies).

We start up our application a bit differently now:

```sh
nodemon index.js
```

#### Params in Express

How do we make our routes dynamic? Using parameters!

Route parameters give us flexibility when writing routes in Express.

Let's update `index.js` to include:

```js
app.get('/:name', (req, res) => {
  res.send(`Hello ${req.params.name}`)
})
```

> Note: the `request` and `response` objects are often shortened to just `req` and `res`.

Our route has changed! What is different?

Route parameters are named segments of our URI, they are placeholders (like variables) that capture values at their location in a URL. These values are held in the `req.params` object and can be used to deliver custom responses to an HTTP request.  

Now if we visit `http://localhost:4000/Whiskers`, we should see:

```
hello Whiskers
```

What do you think we'll see if we visit `http://localhost:4000/Purrasaurus-rex`? 

Where else have we seen these kinds of dynamic segments in routes?

### Views

---
#### Ways to Respond to a Request
<br>

- So far we have responded in our route handler (callback) code by using the `res.send` method.

- The [Express docs for the Response object](https://expressjs.com/en/4x/api.html#res) explains the other ways to respond to the HTTP request.

- Here are the methods we'll use the most:
  - `res.render()` - Render a view template and send the resulting HTML to the browser.
  - `res.redirect()` -	Tell the browser to issue another `GET` request.
  - `res.json()` - Send a JSON response (used when we communicate via AJAX).

---
#### Rendering Views
<br>

- Another of the three fundamental capabilities of a web framework is to be able to use a view engine to render templates.

- A template can include a mixture of static HTML and "code" that generates HTML dynamically.

- For example, code in a template could generate a series of `<li>` elements for data provided to it in an array.

---
#### Rendering Views
<br>

- In Express, we use `res.render` to process a template using a _view engine_ and return the resulting HTML to the browser.

- Express can work with a multitude of _view engines_.

- [`Pug`](https://pugjs.org/api/getting-started.html) (formerly `Jade`) is a template language that leverages indentation to create HTML with a "shorthand" syntax.

- However, [`EJS`](https://www.npmjs.com/package/ejs) (Embedded JavaScript) templates are sweet like bear meat!

---
#### Rendering Views
<br>

- Let's use EJS to render a `home` view for the existing `GET /home` route.

- Express applications are usually architected using the MVC design pattern, so we will put all view templates inside of a `views` folder:

	```sh
	$ mkdir views
	$ touch views/home.ejs
	```

- `ejs` is the file extension for the EJS view engine.

---
#### Rendering Views
<br>

- Open `home.ejs` then type `!` and press tab to generate the HTML boilerplate:

	```html
	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <meta name="viewport" 
	    	content="width=device-width, initial-scale=1.0">
	    <meta http-equiv="X-UA-Compatible" content="ie=edge">
	    <title>First Express</title>
	</head>
	<body>
	    
	</body>
	</html>
	```

---
#### Rendering Views
<br>

- For now, we will need to include the HTML boilerplate inside of every view.

- EJS includes the ability to make our views more DRY by using _partial views_.

- We will cover partial views later, however, if you want to check them out before then, check out the `include` function [here](https://www.npmjs.com/package/ejs#includes). 


---
#### Rendering Views
<br>

- Let's add an `<h1>` inside the `<body>` so that we see something :)

	```html
	<body>
  		<h1>Home Page</h1>
	</body>
	```

---
#### Rendering Views
<br>

- Okay, now let's refactor the `GET /home` route's callback to render our new `home.ejs` template:

	```js
	app.get('/home', function(req, res) {
  		res.render('home');
	});
	```

- Just the file name, not the `ejs` extension.

- Browse to `localhost:3000/home` and - it doesn'twork...

---
#### Rendering Views

- We're going to get a little practice reading Express errors in this lesson.

- The Express error _Error: No default engine was specified..._, makes it clear that we need to specify a view engine.

- This is our first opportunity to configure our app:

	```js
	// Configure the app (app.set)
	app.set('view engine', 'ejs');
	```

- The `app.set` method is used to configure an Express app's settings...

---
#### Rendering Views
<br>

- We also need to tell Express **where** all of our views can be found:

	```js
	// Configure the app (app.set)
	app.set('view engine', 'ejs');
	app.set('views', path.join(__dirname, 'views'));
	```

- Don't be intimidated by this code:<br>`path.join(__dirname, 'views')`...

---
#### Rendering Views
<br>

- `path.join` is just a Node method that builds a properly formatted path from segment strings passed to it. `__dirname` is always available and represents the path of the current folder where the currently running code lives; and `views` is the name of the folder we created to hold our views.

- `path` is a core Node module, but it still must be required before we can use it...

---
#### Rendering Views
<br>

- Core Node modules don't have to be installed with `npm install`, but we do have to `require` them:

	```js
	// Require modules
	const express = require('express');
	const path = require('path');
	```

- Refresh and let's see what the next error is...

---
#### Rendering Views
<br>

- _Error: Cannot find module 'ejs'_ - this error is telling us that we need to install the EJS view engine package:

	```sh
	$ npm i ejs
	```

- We don't need to `require` the view engine - Express knows how to find it.

- Refresh the page - success!

---
#### Dynamic Templating Using EJS
<br>

- Again, view engines are used to dynamically generate HTML on the server before sending it to the client.

- We just used the `render` method, passing in the view name as an argument.

- We can also pass in a JavaScript **object** as a second argument, and all of its properties will be accessible in the view within `ejs` tags!

---
#### Dynamic Templating Using EJS
<br>

- Let's say we want to render a list of To Dos.

- Normally, the To Dos would be coming from a database, however, we'll "fake" a DB by putting the To Dos in a module and export a method to return them.

- Do this to set up the module:

	```sh
	$ mkdir data
	$ touch data/todo-db.js
	```
	
- Next up, put code in the module...

---
#### Dynamic Templating Using EJS
<br>

- In the spirit of saving time, copy/paste the following inside of `todo-db.js`, then we'll review the code:

	```js
	const todos = [
	  {todo: 'Feed Dogs', done: true},
	  {todo: 'Learn Express', done: false},
	  {todo: 'Buy Milk', done: false}
	];
	
	module.exports = {
	  getAll: function() {
	    return todos;
	  }
	};
	```

---
#### Dynamic Templating Using EJS
<br>

- To access our To Do "database", we need to `require` it inside of **server.js**:

	```js
	const path = require('path');
	
	// require the todo "database"
	const todoDb = require('./data/todo-db');
	```

- Now let's add another route responsible for displaying the list of To Do's...

---
#### Dynamic Templating Using EJS
<br>

- Add this new route:

	```js
	app.get('/todos', function(req, res) {
	  res.render('todos/index', {
	    todos: todoDb.getAll()
	  });
	});
	```
	
- Again, to pass data to a view, we pass an object as a second argument to `render`.

- We should now be able to access a `todos` variable in the `todos/index` view...

---
#### Dynamic Templating Using EJS
<br>

- It's a best practice to group views related to a data resource (in this case **To Dos**) in their own folder.

- We also commonly use `index` as a name for views, etc. used for **all** of something - in this case, displaying all To Dos.

- Therefore, we need an `index.ejs` view inside of a `views/todos` folder:

	```sh
	$ mkdir views/todos
	$ touch views/todos/index.ejs
	```

---
#### Dynamic Templating Using EJS
<br>

- Now let's code the `todos/index.ejs` view. Start by copying over the HTML from `home.ejs` and fix it up to look like this:

	```html
	<body>
	  <h1>Todos</h1>
	  <ul>
	    <% todos.forEach(function(t) { %>
	      <li>
	        <%= t.todo %>
	          - 
	        <%= t.done ? 'done' : 'not done' %>
	      </li>
	    <% }); %>
	  </ul>
	</body>
	```

---
#### Dynamic Templating Using EJS
<br>

- That my friends is embedded JavaScript between those `<% %>` and `<%= %>` tags and I believe you are going to love their simplicity!

- The `<% %>` EJS tags are for executing JavaScript such as control flow.

- The `<%= %>` EJS tags are for writing JS expressions into the HTML page.

- Refresh and browse to `localhost:3000/todos` - yeah!

---
#### Redirecting
<br>

- One last trick for the day...

- Currently, if we browse to the root route, we see<br>"Hello Express", however...

- We can use the `res.redirect` method to redirect to `GET /home` so that we will see the Home page upon browsing to the app...

---
#### Redirecting
<br>

- Refactor the root route as follows:

	```js
	app.get('/', function(req, res) {
	  res.redirect('/home');
	});
	```

- Redirects tell the browser to make a new `GET` request to the provided `path`.

- Later, when we  start creating, updating, or deleting data, we will always perform a `redirect`.

---

## You Do: 99 Bottles of Beer

In the time remaining, work through building out an app for the song 99 Bottles of Beer.

The instructions for this exercise can be found [here](https://git.generalassemb.ly/Flex-322/99_bottles_express-).

---
#### ❓ Essential Questions
<br>

Review briefly, then on with the picker:

1. **When we define routes in a web app, we are mapping HTTP requests to ________.**

2. **What method do we call to render a view and on what object does that method exist?**


## Closing

Our first step is to get a basic understanding of Express, how it works and what it does for us. Over the next few lessons, we'll learn how to build larger applications using Express.

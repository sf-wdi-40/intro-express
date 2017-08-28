# Introduction to Express

## Why Express?

- Express is a light framework that gives us functionality to build web applications with Node JS.
- Express allows us to write Node syntax in a more intuitive way.
- Let's check out the [Express JS documentation](https://expressjs.com/).

## Functionality Provided By Express

- **Routing:** The ability to define URI handlers.
- **Middleware (application and router):** Software that is executed before the request-response cycle is completed.
- **Server creation:** Running a web server to handle requests.
- **Extensibility:** Express is extensible through NPM modules and custom modules.

## Starting an Express App

- To begin with Express we must first install it:

```bash
npm install express --save
```

- Next we run `npm init` to create our package.json file.

## Simple "Hello World"

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
	res.send("Hello World!");
});

app.listen(process.env.PORT || 3000);
```

## Route Parameters

- Route parameters are used to identify a resource location.
- They usually describe a RESTful resource.

```
GET http://localhost:3000/users/1
```

- The above should either show a page containing a user with an ID of 1 or return an object representing the user.

## Query Parameters

- Query parameters are appropriately named; they are meant to access the resource as per the route parameters, but filter the results or change them in some way.
- An example would be searching for songs:

```
GET http://localhost:3000/search?track=Hello

GET http://localhost:3000/search?artist=Adele

GET http://localhost:3000/search?playlist=Greatest+Hits&genre=Soul
```

- The first should presumably search for a track called "Hello", the second should return artists matching "Adele", and the third should look for playlists named "Greatest Hits".
- Notice that the route parameters remain the same with each request.

## Server-Side Rendering with EJS

- Server-side rendering essentially means "compiling" and inserting data into templates before they get sent back to the front end.
- This means that the front end will not be responsible for taking JSON data and rendering it with tools such as Handlebars.
- We will have to do a little setup to use EJS:

Install module:

```bash
npm install ejs --save
```

Setup view engine:

```javascript
app.set("view engine", "ejs");
```

Render any template from the application:

```javascript
res.render("index");
```

## RESTful Routing with Express

- Express allows us to set up RESTful routing to handle each of the HTTP request types.
- We will set this up in our application.

```javascript
app.get();

app.post();

app.put();

app.delete();
```

## Handling POST Data with Body Parser

- Express does not do any body parsing out of the box.
- In order to extract data from AJAX/Form requests we will need to use the body parser NPM module:

Install the module:

```bash
npm install body-parser --save
```

Setup the module:

```javascript
const bodyParser = require("body-parser");

app.use(bodyParser.urlencoded({extended: true});
app.use(bodyParser.json());
```

## Using HTML Forms with PUT and DELETE Requests

- HTML forms by default do not support PUT and DELETE requests.
- In order to allow these requests from forms, a technique known as a method override is employed:

Install module:

```bash
npm install method-override --save
```

Setup module:

```javascript
const methodOverride = require("method-override");

app.use(methodOverride("_method"));
```

Use in forms:

```html
<form method="POST" action="/users?_method=put">
</form>
```
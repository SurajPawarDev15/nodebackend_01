# Simple Todo App (Express + EJS)

This repository runs a minimal Express server with EJS rendering and a form to add todos.

## Files

### app.js

```javascript
const express = require("express");
const app = express();

app.set("view engine", "ejs");
app.use(express.urlencoded({ extended: true }));

let todos = [];

app.get("/", (req, res) => {
  res.render("index", { todos: todos });
});

app.get("/about", (req, res) => {
  res.send("<h1>This is the about page!!</h1>");
});

app.post("/add", (req, res) => {
  let title = req.body.title;
  todos.push(title);
  res.redirect("/");
});

app.listen(8000, () => {
  console.log("Server is running on port 8000");
});
```

### views/index.ejs

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Todo App</title>
  </head>
  <body>
    <h1>Todos</h1>

    <form action="/add" method="POST">
      <input type="text" name="title" placeholder="New todo" required />
      <button type="submit">Add</button>
    </form>

    <ul>
      <% if (todos && todos.length) { %> <% todos.forEach(function(todo, i) { %>
      <li><%= i + 1 %>. <%= todo %></li>
      <% }) %> <% } else { %>
      <li>No todos yet</li>
      <% } %>
    </ul>

    <p><a href="/about">About</a></p>
  </body>
</html>
```

### package.json

```json
{
  "name": "simple-todo",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
  "dependencies": {
    "express": "^5.2.1",
    "nodemon": "^3.1.14",
    "ejs": "^3.1.9"
  }
}
```

## How to run

1. Install dependencies:

```bash
npm install
```

2. Start server:

```bash
npm start
```

3. Open in browser:
   http://localhost:8000

## Notes

- The server uses an in-memory `todos` array (not persistent). Restarting the server clears todos.
- `views/index.ejs` must be placed in a `views` folder next to `app.js`.

---

If you want, I can:

- create these files in your workspace,
- add simple styling,
- or switch to persistent storage (JSON file or a small DB). Which would you like next?

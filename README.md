# node_app_checklist
A tl;dr checklist to guide your workflow for your new Node App

### Set Up NodeJS and Express

 - Initialize a new NodeJS application using `npm init -y` (`-y` accepts all default settings)
  -  npm = node package manager

 - `npm install --save express`
  - Install Express node module

### Define App

 - Create `index.js`

 - Require Express module and set up app port

  ```javascript
  var express = require("express")
  var app = express()

  app.listen(4000, () => {
    console.log("app listening on port 4000")
  })
  ```

 - Start server with `nodemon` which automates server reload on file change (server start traditionally done with `node index.js`)
  - _to install nodemon_ enter `npm install nodemon` (install globally with `npm install -g nodemon`)

-----

### Helpful Node Snippets

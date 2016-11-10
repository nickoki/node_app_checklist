# node_app_checklist
A tl;dr checklist to guide your workflow for your new Node App

### Set Up NodeJS and Express

 - Initialize a new NodeJS application using `npm init -y` (`-y` accepts all default settings)
  -  npm = node package manager

 - `npm install --save express`
  - Install Express node module
  - _Note:_ `--save` adds module to `package.json`

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

### MongoDB & Mongoose ODM

 - `npm install --save mongoose`

 - Setting up Schema and connection to the db

  ```javascript
  var mongoose = require("mongoose")

  mongoose.Promise = global.Promise

  var ExampleSchema = mongoose.Schema({
    name: String,
  })

  mongoose.model("Example", ExampleSchema)

  mongoose.connect("mongodb://localhost/<app_name>")

  module.exports = mongoose
  ```

 - Handy MongoDB CLI Commands:
  - _Note:_ be sure `mongod` is running in a separate terminal window
  - `mongo` opens interface
  - `show dbs`
  - `use <name_of_db>`
  - `show collections`
  - `<name_of_db>.<name_of_collection>.find({})` to show all

-----

### Other Helpful Modules

- `body-parser`

- `hbs` (handlebars)

# node_app_checklist
A tl;dr checklist to guide your workflow for your new Node App



## Set Up NodeJS and Express

- Initialize a **new NodeJS application** using Node Package Manager

  ```
  $ npm init -y
  ```

  - (`-y` accepts all default settings)


- Install **Express**

  ```
  $ npm install --save express
  ```

  - _Note:_ `--save` auto adds module to `package.json`


- Create `index.js` in root directory

  - Require Express module and set up app port:

  ```javascript
  var express = require("express")
  var app = express()

  app.listen(4000, () => {
    console.log("app listening on port 4000")
  })
  ```

- Start server with `nodemon` which automates server reload on file change (server start traditionally done with `node index.js`)

  - _to install nodemon_ enter `npm install nodemon` (install globally with `npm install -g nodemon`)



## MongoDB & Mongoose ODM

- Install Mongoose

  ```
  $ npm install --save mongoose
  ```

- In `db/connection.js`, set up Schema and connection to the db:

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

  - _Note:_ be sure `$ mongod` is running in a separate terminal window

  - `$ mongo` opens interface

  - `> show dbs`

  - `> use <name_of_db>`

  - `> show collections`

  - `> <name_of_db>.<name_of_collection>.find({})` to show all



## Making the MEN app MEANer (Angular)

- In `index.js` display root file: `layout.html`

  ```javascript
  app.get("/", function(req, res) {
    res.sendFile(__dirname + "/layout.html")
  })
  ```

- Set up Express to accept AJAX requests:

  ```javascript
  app.use(parser.json({extended: true}))
  ```


- CDN Angular from `layout.html` & add link to your Angular app

  ```html
  <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js"></script>
  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-router/0.3.2/angular-ui-router.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.0-beta.2/angular-resource.min.js"></script>
  <script src="/assets/js/app.js"></script>
  ```

- Example Angular Factory and Controller + Express API Route:

  ```javascript
  // app.js (Angular)
  function ExampleFactoryFunction($resource) {
    return $resource("/api/example/:name", {}, {
      update: { method: "put" }
    })
  }

  function indexController(ExampleFactory) {
    ExampleFactory.query()
                  .$promise
                  .then(example => this.example = example)
  }

  // index.js (Express)
  app.post("/api/examples/:name", function(req, res) {
    Example.findOneAndUpdate({name: req.params.name}, req.body, {new: true}).then(example => {
      res.json(example)
    })
  })
  ```

- Example: [WhenPresident](https://github.com/ga-wdi-exercises/whenpresident/tree/angular-solution)

-----

### Other Helpful Modules

- `body-parser`

- `hbs` (handlebars)

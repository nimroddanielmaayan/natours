# Natours - a Node.js Practice Project

> This project is part of Jonas Schmedtmann's node.js bootcamp course on Udemy

> All of the course notes that I wrote are in this file

> The course slides PDF has a lot of important information, including the theory lectures. They "complete" the notes that I wrote here

> The vscode-setup.md file contains Jonas's recommended vscode extensions and settings for node

## Libraries and Packages Used in the Course

- express
- nodemon
- slugify
- morgan
- dotenv

## Node.js Basics

### General

- Remember, that it's possible to use the dirname variable to get the current directory, no matter where the file is located. This can sometimes be better than using relative paths (like ../ or ./)

- I have to get used to console.logging things to the command line console instead of to the browser console

- In node, every file can automatically become a module

- The nodemon package - remember to use it in every node project

- Reminder: Dev dependencies, which are needed only for development but not for production, should be installed with the --save-dev flag. It makes sense to install all the dev dependencies globally, so that we don't have to install them for every project. To install a package globally, we need to use the -g flag

- Reminder: We can't call dev dependencies directly from the command line. We need to use scripts that we define in the package.json file

- A word about version control: NPM package versions look like this: 1.2.3 with the last being bug fixes, the second being minor updates\feature updates, and the first being major version updates. Note, that only major version updates might break our code, and minor updates are always supposed to be backwards compatible. To make sure that we don't get any breaking changes, we can use the ^ symbol before the version number. This is recommended, and it will make sure that we get all the bug fixes and minor updates, but not the major updates. If we want to get all the updates (at our own risk...), we can use the asterix symbol before the version number, or only bug fixes using the ~ symbol (if we want to be extra careful)

- The "npm updated" command can list all the packages that have updates available

- More info on node version management: https://www.sitepoint.com/quick-tip-multiple-versions-node-nvm/

- It's technically possible to use JS\node in order to program many things, like robots, IOT devices, desktop applications, etc. Like many programming languages, it can compiled to the native machine code of different platforms

- A web application's back end is usually built of a server and a database. A server usually has 3 components: An HTTP server, an application and files. More information in Jonas's slides

- Almost all modern web applications are "dynamic". This means that they are generated on the server right before they are sent to the client, according to relevant data

- "True full stack" developers are getting more and more rare today. Usually, developers specialize in either front end or back end, though it's always good to understand both

- The concept of SSR: Server Side Rendering happens, for example, in an online store where not all items are in stock. The server will check the stock, then render the page based on a template, and then send the page to the client

- API based web apps\CSR: Client side rendering. A more recent approach\architecture that's made possible by the high capabilities of modern web browsers and FE frameworks. In this approach, the server only sends data to the client and the client renders the page. This is the approach that we usually use in React (with the exception of Next.js SSR). This approach is based on creating, sending and consuming JSON data rather than sending entire web pages

- It's important for a good back end dev to know how to build both APIs and SSRs

- An important note: If we want to build a server that will supply the same data to different types of clients (like a browser and also a native mobile app), we need to build an API, not an SSR, since only browsers can recieve and render HTML

- Some companies\people don't even have a front end, and only build APIs in order to sell access to their data to others. This is called a "headless" approach

- In node, we're allowed to send only one response to each request. If we accidentally send two responses, we'll get an error

- Note: Jonas's eslint rules + eslint extention libraries are preety good, I might want to use them in the future. It's recommended to find a configuration for eslint that I will like working with

- There are many different ways and styles with which to write a node application, but the best practices that we have in this course and the MVC architechture are very good parliminary guidelines

- Running node files\code from the command line - main options:
    - npm scriptname (if we have a script in package.json)
    - node filename.js
    - nodemon filename.js (to run with nodemon)
    - node foldername/subfoldername/filename.js --option1 --option2 (to run a file that's not in the root folder, with process.argv option flags. This is useful for running one-time scripts)
    - node (opens the node REPL), and then we can write JS code directly in the terminal
    - node -p "1+2" (to run a single line of code)
    - node -e "console.log(1+2)" (to run a single line of code and also log it to the console)
    - node -v (to check the node version)
    - node -h (to see all the options)

### Command Prompt

- Node REPL: To enter REPL (Read Evaluate Print Loop), go into the terminal and write "node"

- To exit REPL, press CTRL+D

- Use underscore to access the previous output

- Use TAB to check the available methods. It's also possible to use TAB to check available sub-methods, for example: string.(TAB)

### Modules

- Modules are like libraries. They are pieces of code that we can use in our application. We can use modules that are built-in in node.js or we can use modules that are built by other developers

- Modules in node are similar to modules in frontend

- It's good practice to first import the core modules, then the third party modules, and then our own modules

### How Node.js Works

- Node uses single thread and uses async code to handle multiple requests and balance the load. This is why there are a lot of callbacks in node.js. On the contrary, other server-side languages like PHP use multi-threading - a separate thread for each request\user

- We will usually use the async version of the node methods, for example: readFile() instead of readFileSync()

### The File System Module

- The file system module is a built-in module in node.js. It allows us to work with the file system on our computer\server, and do things like create, read, update, delete, and rename files

### The HTTP Module

- The first method of the http module is the createServer() method. It takes a callback function as it's single argument. This callback function will be called every time a new request hits the server. The callback function takes two arguments: req and res. req is the request object, and res is the response object

- The node application will never end if an http server is created. It will keep running until we explicitly stop it. To stop the server, we can use CTRL+C. In the background, an endless loop is running and listening for incoming requests

- If possible, it's always better to read data files\template files once, and save them as a variable, outside of the server callback function. This way, the files will be read and stored in the server's memory only once when the server starts, and not every time a request is made

- It's recommended to use synchronous loading at the beginning of the server application (to make sure that all neccessary data is loaded before continuing), and then use asynchronous loading for the rest of the application

### HTML Templating

- It's recommended to use a pattern, like {%VARIABLENAME%} in order to mark variables in the HTML that will later be replaced by real time data from the back end

### Back End Development - Behind the Scenes

- The first file that is sent from the server to the client is the index.html file. The browser then parses the HTML file, and if it finds any links to other files, it sends additional requests to the server for those files. This continues until all the files are sent

- In the dev tools "network" tab, we can see all the requests that were sent to the server, and also see who initiated the request

### Node.js - Behind the Scenes

- The heart of node.js is the event loop. But heavy tasks that might block the main thread (like file system actions, compresion etc.) are automatically offloaded to the thread pool, which by default has 4 threads but can be set to a maximum of 128

- Node is based on "event driven architecture". This means that everything that happens in node is a response to an event, that usually triggers a callback function

- The event loop works in "ticks" or loops. There's a detailed explanation about how a loop happens, in Jonas's slides. It might sometimes be important to understand it, in some edge cases

- It's also important to understand that the nextTick() functions happens before the next tick PHASE, not before the next new tick\loop

- One of the most important things to keep in mind when working with node is that we should never block or slow down the event loop. On the other hand, setImmediate() happens after the next loop, not immediately. So it's usually better to stick to just one of the two methods (nextTick() or setImmediate()). Usually we'll choose setImmediate()

- Most node methods have a "sync" version, which we'll usually only want to use when we actually DO want our code to block the event loop, for any reason

### Event Driven Architecture

- There are 3 parts to event driven architecture: Event emitters, event listeners, and callback functions

- The emitters emit events, the listeners listen to events and then call the callback functions. Note that each stage might have a one-to-many relationship: One emitter can emit many events, several listeners can listen to the same event, and each listener can call many callback functions

- Because there are no "user events" in backend (like mouse click events), backend events are either network events (like a new request), or custom events that we create ourselves when something important happens. Note that all backend events (built-in or custom) are emitted by instances of the same basic EventEmitter superclass

- Server objects are also instances of the eventEmitter class. This means that we can use the on() and emit() methods on them. Note, that there is no eventListener class in node.js. Instead EventEmitter instances both emit and listen to events. So they are more like event emitters\listeners. For example, server objects listen to requests and emmit responses

### Streams

- Streams are also instances of the eventEmitter class. As such, they also have the on() and emit() methods, etc

- When sending and receiving large amounts of data, it's better to use streams, and not to load the entire data into memory

- One of the key methods in streams is the pipe() method. It allows us to pipe the output of one stream into the input of another stream, while taking care of a lot of the low level logic behind the scenes

- If we don't pipe data streams, we risk a "backpressure" situation, where the data is coming in faster than it can be processed. This can cause a memory overflow and other problems

### Modules in node

- Node almost always uses the CommonJS module system, which is different from the ES6 module system which is used in React. These two systems are different not just in syntax, but also in how they work (from a sync\async perspective). One exception to this is when working with .mjs files (which use ES6 modules), but they're not very common

- Remember, that when we require\import in JS, we don't require\import a file, but a module (which is a function, and also an object)

- Node automatically "wraps" every module in a function, which is called the "module wrapper function", and gives it several built-in objects that include important methods and other things. This is why we can use the require() function in every module(for example), even though we didn't define it anywhere, and even though it's not a built-in function in JS

- Module.exports (or just exports) is an object that is available in every module. It's an empty object by default, but we can add properties to it, and eventually export it

- Because every module in node is actually a function, we can pass arguments to it and also see it's arguments using console.log(arguments)

- When exporting, we don't need to declare "export..." like we do in React. The export object exists by default in every module, including modules that we create ourselves

- When we create a module in node, we write a file which is then converted into a function. Remember, that a function is itself an object, and can have properties and methods like any object

- Note, that when we use module.exports, we won't export an entire object but just a single value (like a string, a number, an array, etc.). To export the entire exports object, we need to use just "exports"

- The subject of caching in node modules: When we require a module, node will cache it, so that it doesn't have to be reloaded and executed for every require(). It's important to know this becaue it might affect how our program behaves

## Async JS

### Async Refresher

- Remember, that a node server application can itself call other servers, and request data via an API. So not only front ends are clients, any server can also be a client

- There are 3 ways to deal with async code in JS: Callbacks, promises, and async\await. Async\await is just promises with syntactic sugar, and it's the best of the three

- Promises are reactive objects that are reactively updated according to the state of their async call. They have 3 possible states: Pending, fulfilled, and rejected

- The way to handle errors in async\await is with try\catch blocks (this is also the default\best practice way to handle errors in JS, in general)

- Behind the scenes, JS uses the Promise constructor to create promises from the Promise superclass

- When using async\await, it's also important to throw an error if the promise is rejected at any point, so that the catch block will catch it and mark the promise as rejected

- Calling async\await functions: A good way of doing this is to use an IIFE (Immediately Invoked Function Expression). This way, we can call the async function immediately, and also use the await keyword inside the IIFE however we need to. This is a good way of handling async functions that interact with each other

- The Promise.all pattern: This is a good way of handling multiple promises that don't depend on each other, and that we want to run in parallel. Remember though that if one of the promises is rejected, the entire Promise.all will be rejected

## Express.js

### Express Basics

- Everything that can be done with express can be done with "vanilla node" and the http module, but express makes everything faster and easier

- It's a convention to set up express in a file called app.js

### Postman

- Postman is like a browser, but it doesn't display HTML - it displays JSON. And it can send any type of request, not just GET requests, like a browser

- To write JSON in a postman request: In the "body" tab, select "raw", select "JSON" from the dropdown menu, and then write the JSON in the text area

### REST Architecture

- Slides 62 - 66 in the PDF cover the basics of REST architecture

- The meaning of a stateless server: The server doesn't store any state data about the client (like logged in, current page, etc.). In other words, the server doesn't know anything about the client. You can also say that the server is "client agnostic".
The server only stores data about the resources (like tours, users, etc.), and any request from the client must contain all the data the server needs to process the request

- It's good practice to create versions of the API, so that if you make changes to the API, you don't break the old version. For example: v1, v2, etc

- The JSEND standard: It's a specification for how to format JSON responses from the server. There are other standards as well

- It's good practice to, after every post request, send a 201 ("created") status code and send the newly created object in the response

- In general, it's important to remember to add a status code to every response

- Any request can take parameters\variables, which are then saved in the req.params object. It's possible to have multiple parameters\variables in a single request. Examples: :id, :tourId, :userId, etc

- Parameters can also be optional. If not specified, they will be undefined

- It's usually easier to send a patch request and not a put request, because with a patch request you only need to send the data that you want to update, and not the entire object. In most cases we could write an entire API without using put requests at all

- The route() method is used to create a new route. It takes two arguments: the path and the handler function. It allows us to neatly organize all the routes in one place. If we also name our callback functions, we can add them as parameters to the calls, and our code will be even more organized

### Middleware

- The core of express is the request -> middleware -> response cycle

- "Middleware" is a function that can modify the incoming request data, or the outgoing response data. It's called middleware because it's "in the middle" between the request and the response

- We can say that in express, "everything is middleware". Every function that has access to the request and response objects is, in fact, middleware. For example, a router function is middleware that's applied only to a specific route\request, and handles the things that should happen between the request and the response

- The middleware that we used is also called the "middleware stack", and the order at which the middleware functions are called is very important

- All middleware finctions end with a "next" method, except for the last one which ends with a send method

- To add middleware, we'll usually want to use the app.use() method at the beginning of the application. This way, the middleware will be applied to every request. If we need middleware that applies only to a specific route, there are ways to do that

- Any custom middleware has access to the request and response objects, and also to the next() method. Every middleware function should end with the next() method, except for the last one which should end with the send() method

- Remember that when we have access to the req\res objects, we can add properties to them and not only read them. In many cases middleware does this

- In the express documentation, there's a list of all the built-in middleware functions that express provides and also the third party middleware functions that are recommended by express

- Param middleware: This is a special type of middleware that only runs for certain parameters. For example, if we have a route like "/api/v1/tours/:id", we can create a middleware function that will run only for this route, and will check if the id is valid. This is a good way of validating data

- Param middleware has access to: req, res, next, val (the value of the parameter), and name (the name of the parameter)

- If the param that we're checking doesn't exist, the middleware will be skipped

- The phillosophy of express is to use middleware and not if-else statements whenever possible, even when if-else statements might also work

### Routing

- The express.Router() method and the pattern that's used with it create a way of separating the routes into different files, and then importing them into the main app.js file. This is a good way of organizing the code

- Routing conventions - Some good practices with routes are:
    - Put all routes in a "routes" folder
    - Name them just "router"
    - module.exports = router; and then give the name in the import
    - Put all route handlers in a "controllers" folder

- It's also good practice to meep all the express stuff in the app.js file, and all the server stuff in the server.js file

- server.js is the entry point to the entire node application. It shouldn't import express (only app.js should do that). server.js should only import the app.js file and then start the server

- Chaining multiple controllers\middleware to one route: It's possible to chain several controllers to one route, and they will all run in order.
For example: checkId -> checkBody -> createTour

### Serving Static Files

- This subject is simple but super important for any web application

- The express.static() method is a simple, built-in middleware function that allows us to serve static files. It takes one argument: the path to the folder that contains the static files

- It's recommended to use the __dirname variable when specifying the path to the static files folder

- When accessing the static files, the folder that we set in express.static() will become the root folder. So it's good practice to only serve static files from one folder that may have subfolders, and not from multiple folders

### Environment Variables

- This is an important core concept in node.js and express

- Environment variables are global variables that define the environment of the node application. Node and express both set a lot of environment variables by default, and we can also set our own

- Every node app must have an env variable called NODE_ENV. It's usually set to "development" or "production". If not defined by us, this variable is set automatically by node to "development"

- To set the env variables in node, we can either add all of them to the command line, or we can use a config.env file (which is the more practical\best practice way)

- It is best practice to put sensitive\secret data like passwords and API keys in the config.env file

- It's a convention to write env names in uppercase, and to separate words with underscores

- The best practice way to apply the config.env is using the dotenv package. This package will automatically read the config.env file and set all the variables in it to the process.env object

- The dotenv package should be required at the top of the server.js file and called using the dotenv.config() method. And that's it, there's no need to add anything to the package.json file (unless we want to overwrite any env variable). This must be done before requiring app.js or anything else that might depend on env variables, otherwise the env variables won't be available for them

- If we do want to overwrite an env variable when strting a script, we need to add the variable to the script in package.json. For example: "start-prod": "NODE_ENV=production nodemon server.js"

- Once dotenv.config() has run, any env variable (like: process.ENV.VARIABLE_NAME) will be available in every file of the application, without having to require anything in these files. That's because dotenv.config() saves the env variables in the global node process object, and they are then read from there

- It's possible (and sometimes useful) to log the entire process.env object to the console, from anywhere in the application

## MongoDB and Mongoose

### MongoDB Basics

- MongoDB is a NoSQL database. It's a document database, which means that it stores data in JSON-like documents called BSON. It's also a non-relational database, which means that it doesn't store data in tables and doesn't use SQL to query the data

- I'm not sure if I need the Mongo Shell or if I can just use Compass. In any case, there are a lot of MongoDB tutorials online for anything that I might need

- It's possible that clients will want to use databases other than MongoDB, so there's no need to know everything about MongoDB, just the basics and the general logic

- Any other information is available online and in the MongoDB documentation

### Mongoose Basics

- Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node. It makes it easier for us to write JS code that interacts with a database (MongoDB in this case)

- It's also possible to write ODM code without Mongoose, but it's more complicated. So Mongoose is like express for MongoDB. There are other ODM libraries for MongoDB, but Mongoose is the most popular one

- Mongoose provides: Data schema (structure) + data model (interface),  validation, queries, middleware and more

- The model wraps the schema and provides an interface between the application and the database, for CRUD operations. A schema is like a blueprint for data (kind of like a class in OOP). In fact, behind the scenes this is exactly what happens - Mongoose creates a class based on the schema, and then we can create new objects from that class. This is a bit of a simplification, but that's the general idea

- Any instance of a model automatically gets built-in methods like save(), find(), etc

- Using the schema and the model, our application will know the "rules" of the database, and will know how to interact with it correctly

- When describing a schema, the minimum that we need to specify are the field name and the field type (using native JS types). For more advanced cases, we can specify the field name and an object of optional values

- To create a schema + model, we first define the schema and then wrap it in a model. The model is then saved in a variable, and we can use it as an API to interact with the database

- It's a convention to begin model names with a capital letter

- If a database doesn't exist, Mongoose will automatically create it once the application requests to create a new document in it

### Advanced Mongoose

- When working with Mongoose, it's recommended to have the docs open and to use them as a reference, since there are a whole lot of methods and options

- Usually, every CRUD action in Mongoose will have 2 stages:
    - Updating the database data
    - Sending a response to the client (so that the client program can update the UI, provide feedback to the user, etc.)

- All of the mongoose methods that we use return promises, so we should use async\await with them

- Create: The best way to create documents with mongoose is using the create() method

- Read: The best way to read documents with mongoose is using the find()\findById()\findOne() methods

- Update: The best way to update documents with mongoose is using the findByIdAndUpdate() method. Note that on this method, it's recommended to set the "new" option to true (which will return the updated document rather than the original) and also to set the "runValidators" option to true (which will run the validators again on the updated document)

- Delete: The best way to delete documents with mongoose is using the findByIdAndDelete() method. Note that it's common practice not to send back any inforamtion to the client about the deleted document, but just a status code

- We need to connect to the database using the mongoose.connect() method before we can do anything else with mongoose, in any file which connects to the database. Because of this, it's best practice to put the mongoose.connect() method only in one file, usually the server.js file

### MVC Architecture in the MERN Stack

- MVC stands for Model-View-Controller. It's a common architecture for web applications

- The controller is concerned only with application logic, the Model is concerned only with business logic, and the view is concerned only with presentation logic. Usually, any input will go through all three of them and end with an output. The controller will usually be the mediator between the model, the view, the input and the output, as we can see in the chart in the slides

- Business logic and application logic might sometimes overlap, but it's important to keep them separate as much as possible, within logic

- "Fat models\thin controllers": A common convention in MVC, which aims to offload as much of the logic as possible to the model. Though in node, the controller will always be needed in order to handle requests and responses, so it won't be completely "thin"
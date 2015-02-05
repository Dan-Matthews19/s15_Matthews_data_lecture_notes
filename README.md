# s15_Matthews_data_lecture_notes
# Lecture Notes for Data Engineering in Spring 2015

## Lecture 1

Prof. Anderson is asking us to create a repo on GitHub and take notes in Markdown. I'm not sure how I feel about this.

Markdown: Need a volunteer to create a presentation about Markdown. Cover basic Markdown... and GitHub's extensions to Markdown.

What do you think about when you hear BigData? Social Networks, data analytics (with many categories i.e. sampling all the way to various classes of machine learning), storage(NoSQL -> came from people having issues with relational database structure. SQL is great when you have a schema for data. NoSQL works better for unstructured data and returning fast results, not very good at doing arbitrary querys.) In NoSQL there are document databases, graph databases, colomnar, key-value stores

Data Modeling is WICKED HARD

There is a space called Data Collection and Cleaning.

A tweet connects to twitter which connects to many twitter clients

Statistics comes bag in BigData analytics. Statistics is built on sampling.

InfoViz: Have huge datasets, how do you display them to the user? D3- javascript framework that helps you do visualizations in the browser. Tabluea, Excell, R are some more examples.

Data Life Cycle: What is your question- curation, triage(medical term for who needs treatment, or resources, more than others), persistance, Collection generation, clean up, storage, processing/analysis. -> query and visualize or ACT -> gives you new questions.

---------
## Lecture 2

Git is the largest, most scalable and powerful VCS for software development. It is considered a Distributed VCS.

Download the github student pack.

### Dustin's Markdown presentation

What is Markdown? A type of Markup language
  plain text formatting that is allowed to easily convert to HTML
  goes from plain text to rich text
  
Two types:
  Standard MD
  GitHub flavored MD
  
What can you do with it?
  Styling
  Word formatting
  Add images
  Create lists (ol , ul)
  LInks
  Code blocks

---

Web browser uses the domain name to figure out which server to contact.

  ex. wwww.something.com/product/10
  
* GET
* POST
* DELETE
* PUT 

Above are the types of requests (GET and POST most common)

Lots of things can be embeded in html files that call for additional requests after hitting enter in URL
  * images
  * scripts
  * href links
  
How to write a service that can accept and assemble JSON and how to write an client side app that accepts JSON

RESTful:
  REST is an architecture or approach for building web services
  Stands for Representation State Transfer
  
URI -- Resources
  URL -> CRUD
  * C: create
  * R: read
  * U: update
  * D: destroy

EX: /users (URI that delivers a set of Data)
  * GET -- Read
  * POST -- Create
  * PUT -- Update (PUT on a particular User ID)
  * DELETE -- Destroy
  
Example of a Request Response cycle

```
curl http://localhost:3000/api/1.0/whattimeisit

```
```
require 'sinatra'
require 'sinatra/reloader' if development?

require 'json'

configure do
  set :port 3000
  ....
  
```

-----
#Lecture 3
##January, 20 2013

###Restful Web Services

  * REST is an approach to developing web services taht mimics the design of the Web itself
  * REST is an architectural style for webservices
  * * invented by Roy Fielding at UC Irvine
  * Your service provides access to a linked set of resources
  * For each resource, you can perform operations on it similar to the main operations (a.k.a. methods) of the HTTP specification.

CRUD (REST HTTP methods)
  * POST - CREATE a resource
  * GET - READ a resource
  * PUT - UPDATE a resource
  * DELETE - DELETE a resource

Examples:
```
GET /api/1.0/users

```
retrieve a list of all users

```
GET /api/1.0/users/0
```
Retrieve the detales of User 0

```
POST /api/1.0/users
```
Create a new user

```
PUT /api/1.0/users/0

```
Update User 0

```
DELETE /api/1.0/users/0
```
Delete user 0

```
GET /api/1.0/search?q=tattersail
```

Perform a search with the query tattersail

Discusion(1):
* Each operation may produce a result
* * With RESTful services, JSON formatting is king
* POST and PUT methods typically send data
  * Also in Json Format
  * May be in the URL or in the body of the HTTP request
    * For GET, the data may appear as query params
* Other formats are possiible: HTML, XML are typical
* Request needs to be authenticated
  * The authentication data appears in HTTP headers

Discussion(2):

How do you think operations on two resources are handled?

One approach
```
GET /api/1.0/posts/0/comments/1
```
* Get the first comment on post 0.
```
POST /api/posts/0/comments
```
* Create a new comment on post 0

Alternative Approach
* While performing an operation on one resource, you reference other resources by ID

ISSUES
* Security: How do you authenticate users? (who can do what)
* Identity: How are ID's assigned to resources?
* Failure: How do we handle failure situartions?
  * In the example today, I handle it in the JSON
  * I could have used HTTP Status codes (404, 500, etc)
  * Most services will use a combination of both.
* Persistence: How are resources stored?

EXAMPLE
* Contacts Web Service
* Implemented in both Ruby and JS
* Technologies used
  * Sinatra - handles HTTP Request (web service framework)
  * Rspec - Testing framework, uses behavioral testing, if something fails, you get back a natural language description of what went wrong.
  * Typhoeus - lib curl wrapper
  * Node - a wrapper around the Chrom JS Engine to execute JS on the server side
  * Express - Framework for node


#Lecture 4, 1/22/15
##Git Version Control System- Open Source

Workflow
* Untracked
  * Theses are not yet in the repo
  * add or gitignore
* initialize repo
* add existing items to the repo
* .....
Workflow with remote
* Clone the previously existing
* pull merge pull then finally push
* rinse and repeat

Initializatoin:

init
Usage:
* git init
  * does the background work to start a git repository in the current directory which has no files currently tracked
Clone
* git clone remote_repo_adress
  * creates a new git repos in the current directory
* git branch- review branches in repo
* git branch new_branch_name- create new branch
* git branch -d name: delete branch
* git checkout branch_name: change to that branch
* git checkout commit: move the current state of your copy to a certain commit
* git add: add stage one or more files, stages for commit
* git commit -m "message": commit with a message
* git merge branch_name: merges the named branch into the current branch

How to resolve conflicts:
* open file with a conflict
* find the conflict
  * conflicts are begun with <<<<<<<<< yours:name of file
  * Differences are separated by =========
  * Conflicts end with >>>>>>>>> theirs:name of file
* ....
Pull and push
* git pull [remote_repo] [branch_name]: two parameters are optional if the defaults are set
* git push [rempot_repo]: pushes all the updated branches to their equivalent in the remote repo
Status
* git status -b
  * this gives the status of the files in the repo
  * the -b flag also provides the name of the current branch
Non-tracked files
* files you do not wish to be part of your repo (typically executables or anything built)
* These files are handled via a file called .gitignore
* this removes unwanted files from being marked as untracked
Log
* gives history of commits
* particularyly usefule for finding the hash to checkout a particular
Remote
* setup remote knowledge of remote repos
Stash
* similar to the concept of shelving in other VCS
Rebase
* a method for changing how branches are related
Diff
* show differences between two states of the repository
Fetch
* get the changes but do not integrate
Reset
* move the current head
tag
* mark git objects
mv
* move a files location within repo
rm
* stop tracking the changes to a file

Branches:
* all a branch is, is a pointer that points at a commit.
* default branch is called master: on initial commit master and HEAD both point there
* if you add another branch i.e. sorting, it creates a pointer called sorting that points at the same commit
* if you make a commmit on the branch sorting, sorting ptr points to new commit and that new commit points to original branch
* HEAD is a pointer on each branch that points to latest commit, on every branch

Rebase(alternative to merge)

-----
##GitHub Presentatoin

Create a branch
* git checkout -b "branch name"
* Anything on the master branch is always deployable to production

Add some commits
* git commit -m "so many monocles"

Open a pull request
* send a pull request to add a branch to master

* use @mention
* use fork/pull model for open sorce repos

Fork
* a fork is an exact copy of a repository
* use it to run experiements without screwing anything up
* Fork vs. clone: clone you can't push back because you don't have colabortator acces, fork creates your own repo copy that you CAN push to.

For vs. Branch
* don't have collaborator access, fork
* if you have collaborator access, branch

Once you have a pull request: Discuss and review code
* remember we are colaborating
* pull request comments support emojis

Merge and Deploy

You can include keywords to automatically close issues

JavaScipt request implementation
* slightly simpler than ruby
* Node: a wrapper around googles javascript engine

-----------
# Lecture 5: 1/27/2015
## Node.js

Node.js is a server side tool and framework for executing JS. wraps googles  JS engine, V8, and makes those features available.
* great for writing webservices
* Most code in node is package inside of a module
* http is a core module, directly built in, provided by Node.js itself
* thttp provides a function createServer()

JavaScript supports first class functions
* functions can be used as variables, parameters, functions that return functions that you can call, etc
* argument in below example is a function.
* listen() takes a port number and server for arguments
```
http.creatServer(<function>).listen(1337, '127.0.0.1');

```
* this is an anonymous function passed to createServer()
* each time server receives a request:
  * it invokes this function and passes the HTTP request and response objects
* this particular function ingores all input and generates and HTTP request or response

```
console.log('Server running at http://127.0.0.1');
```
* console.log, like printf()

Event loop:
* in order to understand Node.js you must understand the event loop
* event-based programming is a style where the code you write is not in control
  * you write handlers for events to control the flow
* Node tries to make it easy to add work to the event que
* Node also lets you add functions to the event queue for later exec
  * process.nextTick()
  * setImmediate()
  * setTimeout()
  * setInterval()

```
console.log('first');
process.nextTick(function() {
  console.log("third");
});
console.log("second");
```
* our main program is simply a function passed to the event loop
* on the first pass: log(), nextTick(), log()
* on the second pass: log()
* since there are no more events, the program ends
Difference between nextTick() and setImmediate()
* setImmediate() allows IO-related callbacks to process first
* nextTick() will prioritize your function before IO-related callbacks, possibly causing IO-starvation

SetTimeout() and setInterval()
* setTimeout() takes second parameter specifying how long to wait before function executed (in miliseconds)
* setInterval() take a second parameter specifying how ofter the function should be executed (in miliseconds)
  * if the interval is never turned off the node will execute forever, look at Node.js documentation on how to stop

Callback Hell
* callbacks are great for asychronous programming, but...
* it can lead to callback hell where callbacks get indented over and over
* two ways to solve this problem:
  * Use sychronous funtions instead (program blocks while function executes)
    * wait for the function to finishing before continuing on in the program
  * used named callback functions

Just Callbacks?
* are callbacks the only asynchronous things in node?
  * NO

Node Execution model
* for user-written code Node is single threaded!
* any code that you write is guarenteed to by synchronous
* you do not have to worry about race conditions
* IO is handled in parallel
    * define functions at the top of the file and refer to them by name in the callbacks

----------
# Lecture 6, 1/29/15
## Express

* web application framework written in JS for use in Node.js
* design influenced by sinatra
* makes it very easy to define endpoints of web-based service
* also has features (such as serving static files) that allow you to create a website
* minimal framework: designed to be augmented by node packages that are then wired in middleware
Express by example:

---------
# Lecture 7, 2/3/15
## Angular JS

* a client-side web app framework written in JS for use in most web browsers
* proveides an implementation of model-view-controllr in the Web Browser to make it easier to produce modular  web clients
* these client side apps are designed to live on top of JSON-based RESTful web services

Not the easiest learning curve
* once we moved beyond simple examples it gets complex fast
* VERY powerful
  * you just to learn core concepts and idioms
  * we will learn ANGULARJS 1.3

Core Concepts
* Data bindings
  * the value of an HTML tag can be associated with a model object stored in a controller. When one changes, angular updates the other automatically.
* Controllers
  * associated with a portion of your HTML -> define all of the state and methods that can be accessed within that section of the page
  * you can modularize your web app and decompose data and functionality into small, manageable chunks
Services
* if you need to maintain state between invocations of a controller or if you need to share state between two different controllers, you can create a service.
* services are created when an Angular app is  initialized
  * they will remain in place for the entire life of the app

Directives
* uiquitous in angular, allow angular to integrate into HTML in a natural way
* can also be used to create re-usable components that combine controllers, data, and HTML
  * you can create a login form component that can be re-used across multiple projects

Embeddable
* angular can control as much or as little of a web page as you specify
* easy to embed a small angular component to existing page and then incrementally expand it

Injectable
* uses dependency injection: injects dependencies without explicitly writing it
* rather than use main routine, angular declares dependencies up front
* angular run-time system locates the dependencies and injects into components that need them

Modules
* primary way to package up a set of controllers into angular app
* create it by giving it a name and litst dependencies

```
angular.module('contactsApp' , [])
```
* this creates a module called contactsApp, this module has no dependencies ([])
* once you create module you can gain a handle to it by calling angular.module with no dependencies
* once module defined in JS, you can tell angular where it lives in html with the ng-app directive

Controllers
* to actually do someting, need controller
* a simple controller may have no dependencies
* more complex controllers will declare dependencies

Why do we do this?
```
var self = this;
```
* closures!
* note that we reference self.message in the function changeMessage()
* if we had said this.message in changeMessage() there is a chance that it no longer refers to a controller.

---------

# Lecture 8, 2/5/2015
## More complicated Angular example

Include all your JS reference at the bottom of the body tag in HTML file, usually all URLs, files, or downloaded packages

```
<script src="js/jquery-1.11.2.min.js"></script>
```

Must link css for specific styles: ex. Bootstrap

```
<link href="css/bootstrap.css" rel="stylesheet">
```
User's route
```
}).when('/users' , {
  templateURL: 'views/users.html',
  controller: 'UsersController as ctrl',
  resolve:{
    verifu: ['UserService , function(UserService) {
      if(UserService.user.admin === false) {
        throw "Not authorized";
      }
      return true;
      }],
      user: ['UserService', function(UsersService) {
        reutrn UserService.refresh(); // refresh() allows you to return a promise, allows for asynchronous calls
      }]
    }
```
refresh function
```
refresh: function() {
  service.users.length = 0;
  var deferred = $q.defer(); // returns promise
  $http.get("/api/1.0/users").then(function (response) {
    Array.prototype.push.apply(
      service.users,
      response.data.users);
    deferred.resolve(response.data.users);
  }, function(error) {
    deferred.reject();
  });
  return deferred.promise
}
```

So far:
* web services
* put something on client side that allows us to build website
* carefully controlled interactions with server such as loggin info




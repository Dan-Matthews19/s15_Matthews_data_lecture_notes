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

---------
#Lecture 9, 2/10/2015
## Getting Data from Twitter

Two helpful books:
* principles of object-oriented javsscript
* secrets of the javasscript ninja

Contacts web_app
* link on github to contacts web_api

RequireJS:
* RequireJS implements the AMD (Asynchronous Module Definition) spec, which means we can write our own modules and load them with RequireJS, allowing it to manage dependencies for us.
*  Have you ever had multiple script tags and had to load them in a particular order as one relied on the other? I have, and it's a nightmare. Working in a modular fashion really eliminates this issue and in this tutorial I hope to demonstrate just how.
*  controllers.js: define is the requirejs, all the middle code is angular

Applied to the web abb:
* each controller is in its own file and all stored in their own seperate module
* I combined my two services into one service
* ...

IIFES
* the code in the new app now follows a common convention in JS known as the module pattern
* this is also known as the immediately invoked function expression (IIFE).

Getting Data From Twitter part 1:
* first thing we need to do is to create an account on Twitter
  * created data_at_cu for this class
* Make sure and set up account before thursday
* Next head to https://dev.twitter.com (site for twitter developers)
  * Scroll to the bottom and click on manage your apps
  * loggin --> create new app
Created Twitter app on dama8893_dev account

-------
#Lecture 10 Getting Data from twitter take two
## 2/12/15

Showed up a little bit late so fell behind in the demo. Follow lecture 10 slides to get back up to speed.
Download:
* ruby
* gem
* recomended: rbenv

Laptop dying. Will pick up next lecture

-----------

#Lecture 11 Twitter Data Collection Framework
## 2/17/15

This framework will allows to access the search API, shows two implementations of accessing the streaming API

Twitter framework now available on the class GitHub
* examples of implementations of five REST API endpints and two streaming endpoints
* automatically handles twitter rate limits
* provides implemenations for working with timelines and working with cursors
* In lecture 10 we reviewed the code that was needed to make a single GET request on a single REST API

High-level view of framework
* apps --> requests --> core --> helpers

Twitter request
* standardized constructor
* expects an args hash with up to three entries
* sets the contract required by all sub-classes

Contract?
* In a statically typed language like Java, we would use interface
* in a dynamically typed language like ruby, we improvise
```
def url
  raise NotImplementedError, "no URL Specified for the Request"
end
```

* A twitter request has a public collect method that yeilds collected data back to its caller

Helpers:
* Params and Props
* Logging and Rates

Params and Props:
* Only two new features
  * the ability to control if a parameter is included in a request
  * the ability to display the parameters that are being sent with a request

Logging
* the logging helper consists of a custom class definition and a method to create a default logger

Ruby logger:
```
require 'logger'
```
* the logger is createer in TwitterRequest's constructor
```
@log = args[:log] || default_logger
```
Rates
* rates helper allows the framework to automatically keep track of rate limits for a given Twitter endpoint
* the default make_request ensures that the rates are checked on each request
* user auth request rate = 180 request / 15 minutes (one request can recieve about 200 tweets)
* the rates helper invokes a Twitter endpoint to get the applications current set of rate limits
* these rates are stored in a class variable (static) (@@var_name in ruby) so they are shared across all TwitterRequests instances created by an app
* these global rates are only refreshed when needed

Types of Requests:
* framework has the following sub-classes:
* max-idRequest:
  * A subclass for endpoints that need to traverse timelines with the max_id parameter
```
params[:max_id] = (tweets[-1]['id'] -1) if tweets.size > 0
```
  * Timeline and Search make use of this sub-class maxIdRequest

Example of a search endpoint:
```
def twitter_enpoint
  "/search/tweets"
```
CursorRequest:
* does not need to define a contract for subclasses
* it can implement all of the required functionallity directly
```
params[:cursor] = -1
```
StreamingTwitterRequest:
* collect method is designed to run forever (while(true))
* we use Typheous to create a request and then define a series of event handlers on the request
* handlers get called when appropriate as data streams in
  * on_headers: lets us check to see if we successfully established connection
  * on_body: some data has been revieced from server; we need to process it
  * on_complete: the response has finished; clean up before quit
* The client can also request a shutdown: call request_shutdown
* on_body uses a lower level buffer to collect data from the server until it is full and then sends it to process method
* there is no guarentee that the data from the buffer actually ends directly on a message boundary

Now showing the twitter framework code

------
#Lecture 12 Introduction to NoSQL
##2/19/15

Two Useful books:
* Big Data: Principles and best practices of scalable realtime data systems, by Nathan Marz and James Warren
* Making Sense of NoSQL: A guide for managers and the rest of us, by Dan McCreary and Annn Kelly

Scaling with Traditional Databases:

Web Analytics Application
* You have a system that will keep track of page views for a number of websites
* when someone loads a page on your client's website it pings your service and you increment the count associated with that URL
* Get lots of customers and lots of pings
* Get error: your system is timing out on the ping request
* so many requests coming in at once: relational data base cannot mutate rows fast enough (i.e. writes)
* spending so much time on writes, it can't keep up with the read request

Instead:
* let aton of request come in, then batch updates to the database, asking it to update multiple rows with each request
* Add a queue between your web server and the code that will update the database
* attach a single worker to the queue that reads 1000 updates off the queue and then inserts them all into database at once

Not a true solution:
* too much data even for worker to handle --> request to mutate rows time out system
* could try to add more workers to the queue but it won't work, because there is still only one database
* the database is a BOTTLENECK
* What is the answer to this problem in relational world?
  * Vertical scaling: will temporarily relieve the pressure and eventually will fail
* Answer: SHARD the database
  * this means that you need multiple copies of the database ( each with own file system )
  * You then partition your data across these databases
  * develop a partitioning strategy
    * often, you will take an MD5 hash of some aspect of the input data and then mod that value by the number of shards
    * then write data to indicated shard
    * do the same thing for reads to locate data needed to fulfill request

Problems:
* if more or less shards created, application (SE) has to manage that including shutting down system to re-SHARD
* if one machine goes down, the entire system goes down
* Fault tollerance is hard
* complexity is pushed to the application layer, application must manage all theses issues
* the lack of human-fault tollerance: Nothing preventing user error to losing data
* Maintenance is an enormous amount of work

NoSQL to the rescue!
* NoSQL databases are ones which are aware of their distributed nature
  * mangage sharding and replication for you
  * horizontally scalable
      * if you need more diskspace add a server
      * need faster computaion, add a server
      * when you add a sever, NoSQL will reshard for you automatically!
* tend to avoid mutable data
  * once data is written, it is immutable and can't be updated
  * if the value changes you write new immutable copy of the updated data and...
  * when you read that value you adopt a strategy of returning the most recently written value
* NoSQL databases are fault tollerant
* this means that all these issues are handled in the database, not at application level
* all of these things happen in the persistence tier

Types of NoSQL
* key-value
* graphs
* columnar
* documents

Key-Value:
* simple database when presented with a string (key), returns an arbitrarily large set of data (value)
* kaey value stores have no quesry language. They act just like hash tables
* values are untyped
* simple!
* examples: Amazon SimpleDB, S3, Redis, Voldemort, Riak

Graph Stores:
* databases optimized to store graph structures rather than table/row/column structures
* provide structural query languages so you can locate information based on the structure of your data
* Example: find all pairs of Person nodes who have atleast 3 children together, live in Colorado, and have been married for more then 15 years
* Provide ability to do graph traversals efficiently
* provide ability to calculate shortest paths between two given nodes
* examples: Neo4j, Titan, Infinite Graph, Info Grid

Columnar Stores:
* also know as column family stores
* able to scale to enormous amounts of data
* often able to achieve very fast writes (miliseconds) while also maintaining reasonable read performance
  * Consider: Netflix uses Casandra to store and serve its movies
  * In this case, what you are reading from the database is an entire movie that is then streamed across the internet
* Basic Data model:
  * column family: think of this as a table of related data
  * column families consist of rows that have unique row keys
  * rows consist of columns (potentially millions)
  * columns consist of key and value 
  * value itself might be a JSON map that in turn has keys and values
* Hash tables all the way down
* More acurately: a distributed hash table which is easy to partition across the nodes of a cluster
* Examples: Hbase, Casandra

Document Stores:
* insert documents (a bag of key-value pairs)
* each doc gets indexed in a variety of ways
* Documents can then be found via queries on any attribute
* documents can be grouped into collections, can be grouped into databases
* each database is then used by a particular application to get its work done
* Examples: MongoDB, CouchDB, Solr/Lucene

Why NoSQL?
* implicit in what we have been saying is that there is no schema
  * there is nothing that says: in column 5 of table 2, you will find and INT;
* You are often free to store ANYTHING in one of these databases
* Examples
  * Document stores: each doc in a collection can have a different set of key-value pairs
  * Columnar stores: each row in a columnar store can have different columns
  * a graph database is just a colleciton of nodes and edges. You can add any amount of metadata to each concept to suit your needs.


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




  


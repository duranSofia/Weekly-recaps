# week-10-recap

Material covered at Wild Code School on the first online week

# Express

Express is a lightweight framework built for Node, that simplifies web development.
It provides extra tools for building web applications, the most common functionalities are:

- managing outside connections (e.g. http requests)
- reading from and writing to a database
- sending html and json files

**minimalist Express server**:

```
const express = require('express');
const app = express();
const router = express.Router();

router.get('/', (req, res) => {
 res.send('Hello World!')
});

app.use('/', router);

app.listen(3000, () => {
 console.log('Example app listening on port 3000!')
});
```

**Http methods with the router**:

get()
post()
put()
delete()

```
router.get('/', () => {});

router.post('/', () => {});

```

**More routing methods**:
copy
head
lock
merge
mkactivity
mkcol
move
m-search
notify
options
patch
purge
report
search
subscribe
trace
unlock
unsubscribe
source: (https://expressjs.com/en/4x/api.html#app.METHOD)

The method, app.all(), is not derived from any HTTP method and loads middleware at the specified path for **all** HTTP request methods.

**Multiple routers**:

We can split our routes into multiple routers.

As an example:
we have a router for handling all the static pages like home, about, contact, etc
and a router for the dynamic pages like trips:

```
const homeRouter = express.Router();
const tripsRouter = express.Router();

homeRouter.get('/', (req, res) => {
   res.send('Welcome to Lisbon')
});

homeRouter.get('/about', (req, res) => {
   res.send('About us')
});

tripsRouter.get('/', (req, res) => {
   res.send('All our trips')
});

tripsRouter.get('/:id', (req, res) => {
   res.send(`Trip number ${req.params.id}`)
});

app.use('/', homeRouter);
app.use('/trips', tripsRouter);

```

# Middleware

Middleware is software that lies between an operating system and the applications running on it. Essentially functioning as hidden translation layer, middleware enables communication and data management for distributed applications. It’s sometimes called plumbing, as it connects two applications together so data and databases can be easily passed between the “pipe.” Using middleware allows users to perform such requests as submitting forms on a web browser, or allowing the web server to return dynamic web pages based on a user’s profile.

Common middleware examples include database middleware, application server middleware, message-oriented middleware, web middleware, and transaction-processing monitors.
source: (https://azure.microsoft.com/en-us/overview/what-is-middleware/)

**Middleware anatomy**

A middleware function takes 3 arguments: **request, response and next.**

request: an object containing all the data that came in the http request

response: an object with data and functionality for the response

next: a function that can be called to go to the next middleware

```

const getAllTrips = (req, res, next) => {
   // get all trips from the db
   next();
}

tripsRouter.get('/', getAllTrips, ...);
```

**The middleware flow:**

1. getAllTrips()- (req, res)

2. then it calls next()- Expresss automatically sends req and res to the next middleware - showTrips()

```
const getAllTrips = (req, res, next) => {
   // get all trips from the db
   next();
}

const showTrips = (req, res, next) => {
   // render the View responsible for the trips
   // aka: show the trips
}

tripsRouter.get('/', getAllTrips, showTrips);

```

# Accessing request data

The request object contains all the information sent by the client to the server .
e.g.: the sent parameters, the data of a form, the url parameters, the HTTP header, access tokens, etc.

```
router.get('/', (req, res) => {});
```

The 3 most common ways for a client to send information to a server are through:
URL parameters - req.params
a URL query - req.query
a request body - req.body

**URL parametres**

```
// http://localhost:3000/trips/12/photos/23
tripsRouter.get('/trips/:id/photos/:photo_id', (req, res) => {
   res.send(`This is photo ${req.params.photo_id} of trip number ${req.params.id}`)
});
```

**URL query**

```
// http://localhost:3000/trips/search?duration_min=2&price_max=25
tripsRouter.get('/trips/search', (req, res) => {
   res.send(
       `We'll query the database with
       price_max of
       ${req.query.duration_min} and
       dration_max of
       ${req.query.price_max}`
   )
});
```

**Accessing the body of a request**
By default we cannot access body, we need body-parsing middleware such as express.json() or express.urlencoded().

```
tripsRouter.post('/trips/new', (req, res) => {
   const formInputs = req.body;
   // save it to db
   res.send('New trip saved successfully!')
});

app.use(express.json());

```

**Sending the response**:

The response object contains all the information the server will send to the client.
e.g.: html, data from a database, status codes, error messages, the HTTP header, access tokens, etc.

```
router.get('/', (req, res) => {});
```

**Some statuses**:

```
res.send('Hello')
res.status(404).send('Cannot find trip with this id');
res.status(400).json({
    error: 'Missing field "duration_hours"'
})

app.use('/', tripsRouter);

```

with our feline friends: (https://http.cat/).

# REST API

**What is an API?**

It is like a server in a restaurant: takes the order from the customers (computers) and passes it to the kitchen (server). When the order is ready, it is "served".

With more technical terms:
An Application Programming Interface or API is an interface between two computer programs.
It helps developers write programs that are more maintainable and can easily communicate with other pieces of software.

Examples of an API:

Google Chrome: it communicates with many of your operating system’s API’s to be able to access the internet, display stuff on the screen, get keyboard and mouse inputs, access the camera, the speakers, etc.

**Web API**
A Web API is the interface of a webapp with which an external program can communicate.
In short, it’s a server that accepts http requests and responds with json.
It makes our app/service available to many clients over the internet.

**REST API**

REST is a standard for designing web APIs - RESTful APIs.
It is a short for: Representational state transfer.
Set of conventions and best practices to or building web interfaces.

Roy Fielding defined REST in his 2000 PhD dissertation "Architectural Styles and the Design of Network-based Software Architectures" at UC Irvine.

REST describes the following (among other things):

- how to build URIs for each resource
- what HTTP verbs to use for each operation
- how data is received and sent in each resource

Alternatives to REST are SOAP (Simple Object Access Protocol) and GraphQL.

GraphQL is more "hyped" nowadays: an open-source data query and manipulation language for APIs, and a runtime for fulfilling queries with existing data. GraphQL was developed internally by Facebook in 2012 before being publicly released in 2015.

**How to build the URI**

Get a users list:
http://mywebsite.com/users

Get all reviews of an item:
http://mywebsite.com/items/321/review

Get user info:
http://mywebsite.com/users/56

Get a user review:
http://mywebsite.com/items/321/reviews/14

**How to build the URI**

Filtered and sorted list of users:

http://mywebsite.com/users?filter=client&sort=asc

**http://mywebsite.com/items/56/reviews/14**

**HTTP Response Formats:**

The response can come in many formats: HTML, XML, JSON, JSON-LD, CSV, etc.
It is up to the client to define the format it accepts via the Accept header (it can accept multiple formats)

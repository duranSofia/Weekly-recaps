## What is a Higher-Order Component or HOC?
A higher order component is basically a function that takes a component and returns a new component. It transforms a component into another component and adds additional data or functionality.

```javascript 

import React from "react";

const withSecretToLife = WrappedComponent => {
  function HOC() {
    return <WrappedComponent style={{ color: "red" }} secretToLife={42} />;
  }
  return HOC;
};
```

Our function, **withSecretToLife** takes a component **WrappedComponent** as its argument and creates a new component **HOC** that returns **WrappedComponent**.

```javascript 

const DisplayTheSecret = props => (
  <h1 style={props.style}>The Secret of life is {props.secretToLife}</h1>
);

export const HeaderWithSecret = withSecretToLife(DisplayTheSecret);

```

Next we create a new **HeaderWithSecret** component that will call our **withSecretToLife** function with **DisplayTheSecret** as its argument which will get the props from the **WrappedComponent**

It is important to know HOC-s because Redux's primary function **connect** is a Higher Order Component. **connect** accepts a component as its argument and returns a component connected to the Redux store. 



## What is MongoDB?

MongoDB is a document-oriented schema-less NoSQL database used for high volume data storage. It means you can store JSON documents in it, and the structure of these documents can vary as it is not enforced like SQL databases. This is one of the advantages of using NoSQL as it speeds up application development and reduces the complexity of deployments.

**The differences between SQL and NoSQL**

SQL:

* Relational Database management system
* Vertically Scalable
* Fixed or predefined Schema
* Not suitable for hierarchical data storage
* Can be used for complex queries

NoSQL:

* Distributed Database management system
* Horizontally Scalable
* Dynamic Schema
* Best suitable for hierarchical data storage
* Not good for complex queries

**MongoDB installation**

![Imgur](https://imgur.com/4o5Nl5Y.png)

**What is Mongoose?**

Mongoose is a MongoDB object modeling tool designed to work in an 
asynchronous environment. 

**What is an Object Modeling Tool?**

It's a way for us to interact with the database. Mongoose acts as an intermediate between MongoDB and server side language eg. like NodeJs it has to be installed npm i -S mongoose.

**How to define a schema**

![Imgur](https://imgur.com/2IM94AP.png)

* The schema is an object containing the description of a model
* String, Number, Date, Buffer, Boolean, Mixed, ObjectId, Array

**How to connect to a database** 

![Imgur](https://imgur.com/3yrihIe.png)

* The login url can contain the login/password, for use if the database is authenticated: 
mongodb://login:password@localhost:27017/base

**Some keywords**

![Imgur](https://imgur.com/afmAuIX.png)

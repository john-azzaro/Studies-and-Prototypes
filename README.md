# Mongoose CRUD Operatations Study
> *IMPORTANT: This study is a continuation of the Mongoose Configuration and Data Modeling Study. If you want to find out more about configuration of a Mongoose server, build schemas, models, virtuals, and instance methods, click [here](https://github.com/john-azzaro/Study-Mongoose-Configuration-and-Data-Modeling "Link to Mongoose Study").*

<br>

## What is the Mongoose CRUD Operations Study
The Mongoose CRUD Operations study is an examination of built-in methods that Create, Read, Update, and Delete information from the MongoDB database. The following outline follows the book and bookSchema project from the previous study, but also take a look at the restaurant prototype project in the repo.

Here's some questions covered in the study:

* [What are CRUD operations for Mongoose?](#What-are-CRUD-operations-for-Mongoose)
* [How do you CREATE a document using Mongoose?](#How-do-you-CREATE-a-document-using-Mongoose)
* [How do you FIND documents using Mongoose?](#How-do-you-FIND-documents-using-Mongoose)
* [How do you FIND BY ID using Mongoose?](#How-do-you-FIND-BY-ID-using-Mongoose)
* [How do you FIND BY VALUE using Mongoose?](#How-do-you-FIND-BY-VALUE-using-Mongoose)
* [How do you UPDATE a document using Mongoose?](#How-do-you-UPDATE-a-document-using-Mongoose)
* [How do you DELETE a document using Mongoose?](#How-do-you-DELETE-a-document-using-Mongoose)

<br>

## What are CRUD operations for Mongoose?
<dl>
<dd>

CRUD operations are common HTTP methods for communicating with a given server. CRUD operations allow you to make queries in the server's JavaScript code using Mongooseand can be peformed anywhere in your code. For example, the *read* CRUD operation refers to when the client request a document and send a *GET* request. 

In the case of this study, Mongoose has a few ways to *get* the document (stored on MongoDB). This applies to *create* (i.e. POST), *update* (i.e. PUT), and *delete* (i.e. DELETE) as well.

</dd>
</dl>

<br>

## How do you CREATE a document using Mongoose?
<dl>
<dd>



</dd>
</dl>

<br>

## How do you FIND documents using Mongoose?
When you *find* a document, you are essentially reading the documents from the database. In the example below, the client is sending a GET request to the /books endpoint to return 10 books.

<dl>
<dd>

### STEP 1: Create a GET route:
First, we need to send a GET request to the /books endpoint.
```JavaScript
    app.get("/books", (req, res) => {
        // code goes here.
    });
```

### STEP 2: Call the model with the .find method:


```JavaScript
    app.get("/books", (req, res) => {
    Book.find()
        // we're limiting because restaurants db has > 25,000
        // documents, and that's too much to process/return
        .limit(10)
        // success callback: for each restaurant we got back, we'll
        // call the `.serialize` instance method we've created in
        // models.js in order to only expose the data we want the API return.    
        .then(books => {
        res.json({
            books: books.map(books => books.serialize())
        });
        })
        .catch(err => {
        console.error(err);
        res.status(500).json({ message: "Internal server error" });
        });
    });
```

</dd>
</dl>

<br>

## How do you FIND BY ID using Mongoose?
<dl>
<dd>



</dd>
</dl>

<br>

## How do you FIND BY VALUE using Mongoose?
<dl>
<dd>



</dd>
</dl>

<br>

## How do you UPDATE a document using Mongoose?
<dl>
<dd>



</dd>
</dl>

<br>

## How do you DELETE a document using Mongoose?
<dl>
<dd>



</dd>
</dl>
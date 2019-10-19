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
    app.get("/books", (req, res) => {                                  // GET request to /books endpoint.
        ...
        ...
    });
```

### STEP 2: Call the model with the .find method:
When you call ```Books.find()```, by default will retrieve all the documents in the collection.
```JavaScript
    app.get("/books", (req, res) => {
       .find()                                               // Find all documents in the Book collection.
       ...
       ...
    });
```

### STEP 3: Add any additional methods before success callback:
Sometimes, you have to narrow down the scope of the documents you find in the database. For example, suppose you had a database with hundreds, if not *thousands* of documents. In cases like those, you want to limit the return to only a few documents.
```JavaScript
    app.get("/books", (req, res) => {
        Book.find()
            .limit(10)                                                   // Limit return to 10 documents.
            ...
            ...
    });
```

### STEP 4: Success callback!
If the request is successful, we use the ```.then``` method. This will send and object with the property ```books``` whose value is an array of ```books``` objects. Then, for each```books``` we get back (i.e. ```books.map()```) from the collection query, call the ```.serialize``` instance method (see the serialize instance method from models.js) so that only certain info will be exposed when the API returns the data (i.e. does not return sensitive information).

```JavaScript
    app.get("/books", (req, res) => {
    Book.find()
        .limit(10)
        .then(books => {                                                // successful callback
        res.json({
            books: books.map(books => books.serialize())
        });
        })
        ...
        ...
    });
```

### STEP 5: And if there is an error, catch as an error:
If there is an error with the GET request, log an error and a 500 status code (server error) message to the client.
```JavaScript
    app.get("/books", (req, res) => {
    Book.find()
        .limit(10)
        .then(books => {
        res.json({
            books: books.map(books => books.serialize())
        });
        })
        .catch(err => {                                                 // catch error (if any).
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
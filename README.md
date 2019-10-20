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
When you *find* a document, you are essentially reading the documents from the database. In the example below, the client is sending a GET request to the /books endpoint to return 10 books. The way we do this is as follows:

1. **Send a GET request** to the endpoint ```/books```.
2. **Find ALL the documents** at the ```/books``` endpoint.
3. **Only get the first 10 documents** from the ```/books``` endpoint.
4. **If successful, send a response with an object** whose value is an array of ```books``` and for each book in the, apply the 
   ```serialize``` instance method so that only the information you want is sent back as a response.
5. **If unsuccessful, send error message** with server error.

So to put this into practice, start by creating a GET route:

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
       Books.find()                                          // Find all documents in the Book collection.
       ...
       ...
    });
```

### STEP 3: Add any additional methods before success callback:
Sometimes, you have to narrow down the scope of the documents you find in the database. For example, suppose you had a database with hundreds, if not *thousands* of documents. In cases like those, you want to limit the return to only a few documents with the ```.limit``` method. The ```.limit``` method takes one parameter, which is a number defining how many documents to return (i.e. 10).
```JavaScript
    app.get("/books", (req, res) => {
        Books.find()
            .limit(10)                                                 // Limit return to 10 documents.
            ...
            ...
    });
```

### STEP 4: Successful callback!
If the request is successful, we use the ```.then``` method to *return a promise* (from models.js). This will send an object with the property ```books``` whose value is an array of ```books``` objects. Then, for each```books``` we get back (i.e. ```books.map()```) from the collection query, call the ```.serialize``` instance method (see the serialize instance method from models.js) so that only certain info will be exposed when the API returns the data (i.e. does not return sensitive information).

```JavaScript
    app.get("/books", (req, res) => {
    Books.find()
        .limit(10)
        .then(books => {                                                      // successful callback
        res.json({
            books: books.map(books => books.serialize())
        });
        })
        ...
        ...
    });
```

### STEP 5: And if there is an error, catch as an error:
If there is an error with the GET request, send a response with a 500 status code (i.e. server error) and a message to the client saying that there was in fact a server error.
```JavaScript
    app.get("/books", (req, res) => {
    Books.find()
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
With **find by ID**, your objective is to find an *exact match* for your query. Then the server will send back a single object representing the requested book. In this example, we're finding a book by id. This is how we do it.

1. **Send a GET request** to the endpoint ```/books:id```.
2. **Call the model with the ```.findById```**.
3. **If the callback is successful**, return a json string with an object of the book.
4. **if unsuccessful**, send an error message.

<dl>
<dd>

## STEP 1: Create a GET route:
Almost identical to the standard ```.find``` route, only this time we are adding an ```/:id``` to the endpoint. 
```JavaScript
    app.get("/books/:id", (req, res) => {             // get request to the /books/:id endpoint.
        ...
        ...
    });
```

## STEP 2: Call the model with the ".findById" method:
Again, almost identical to th the ```.find``` route, except we want to find the document by id and pass in the user requested endpoint.
```JavaScript
    app.get("/books/:id", (req, res) => {
    Books                                              // from imported model (models.js)...
        .findById(req.params.id)                       // ... find by id parameter provided by user.
        ...
        ...
    });
```

## STEP 3: Successful callback! 
If the promise is successful (i.e. if the get request to the endpoint is valid and the id is found), *then* the reponse will be a json object of the book
which has been processed through the ```.serialize``` instance method
```JavaScript
    app.get("/books/:id", (req, res) => {
    Books
        .findById(req.params.id)
        .then(books => res.json(books.serialize()))    // return a json string representing the object
        ...                                            // produced by the Books serialization method.
        ...
    });
```

## STEP 4: If unsuccessful, send back error:
And of course, if there is an error, send back a 500 internal server error asd a response with a message.

```JavaScript
    app.get("/books/:id", (req, res) => {
    Books
        .findById(req.params.id)
        .then(books => res.json(books.serialize()))
        .catch(err => {                                                       // send error if needed.
        console.error(err); 
        res.status(500).json({ message: "Internal server error" });
        });
    });
```


</dd>
</dl>

<br>

## How do you FIND BY VALUE using Mongoose?
When you find by value, that is, find by optional requests such as author and book or book and isPublished, you need to use```findByValue```. There is a little more to ```findByValue``` than the previous READ operations you need to do:

1. 


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
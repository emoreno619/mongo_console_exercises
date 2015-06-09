## Mongo Concepts + Console Exercise 

For tonight's assignment, we'd like you to answer a few questions and define a couple terms as well as write the queries necessary to perform the following tasks. You can either fork and clone this readme or create a new one with your solutions.
You will be using the terminal and the mongo shell for this assignment as well as notes/google to answer some of the questions


## Part I - Conceptual Review 

Define these terms and answer these questions in 1-3 sentences (some will require a bit of googling)

### Terms

* Database

A database is a server that stores information. There are different types of databases; relational and non-relational databases are one of the main differences. Mongo is non-relational, which means that the data stored within the database has few rules or structure they must follow (unlike relational databases).

* Collection

A collection is a loose form of organization within a MongoDB. It is roughly analogous to a table, in that is the top-most layer of organization of data besides the database itself. In Mongo, a collection is comprised of documents (which can--but not need--be individual pieces of data).

* Document

A document is the next layer of data beneath database and collection. Each document has individual unique identifies attached to it, but a document can store more than one piece of data, because in Mongo all data (and documents specifically) are stored as objects. So, each object can contain many pieces of information.

* Cursor

A cursor is a pointer (or location within memory) to the results of a query. A query is solicits the database for certain kinds of data; it could be all of the data or individuals pieces of data matching certain criteria. In either case, Mongo returns a pointer to the results of the query because it is faster and less cumbersome to return a pointer to the data rather than the data itself.
 
* Field

In Mongo, a field is the identifier or key for a value of an object (or document). So 'document' is to 'object', as 'field' is to 'key'.

* CRUD

The acronym CRUD stands for Create-Read-Update-Delete, which are the standard processes involved when interacting with a database. 

* Relational Database

A relational database typically has stricter rules and structure than a non-relational database. A relational database contains certain parts of data that are shared (and so repeated) across different tables (or collections) in order to 'relate' the data among them to one another.

* Non-Relational Database

A non-relational database need not have the same strict structure or overlap of data across different parts of the database. This makes adding data that is new or different from other data within the database much easier, since it need not worry about structuring the database beforehand, but it also results in the database being less organized and potentially more difficult to navigate.

* CAP Theorem

The CAP theorem refers to three ideal properties of a distributed computer system (which could be a database stored across multiple servers). CAP stands for: consistency, availability and partition tolerance. 

Consistency refers to each server having access to all of the same data as each other server. Of course, if one server receives new data, no matter how fast the connection between the servers, there is always some delay between them, so 100% consistency among a group is impossible. 

Availability refers to each server be in complete communication and 'available' to the requests of the others (a form of reliability). But again, there is always a delay in communication (or perhaps even a server failure) that cannot be offset completely by data back up redundancy.

Partition tolerance refers to the strength of a distributed system to endure failures within the system. For example, a system with three servers (A, B, C) where the only connection between A and C is via B would be less fault tolerant to a failure of B than would a system where A and C can communicate directly or via B.

* Schema

A schema is a form of organization or stucture within Mongo, roughly analogous to a table in SQL in that is unite certain data, but in Mongo a schema is foremost flexible. So, a schema is a way of relating data (collections or documents) to one another in a more flexible way than traditional relational databases (for example even if there is great variation in the structure of the data to be related).

### Questions

* Do MongoDB databases have schemas?

Yes, MongoDB has schemas, and they are flexible.

* What are typical uses for MongoDB?



* What is Mongoose?
* What is a Mongoose Model?

## Part II - Challenges 
Write the queries necessary to perform the following tasks

1. Write the terminal command to start the mongo server

mongod

2. Write the terminal command to enter a mongo shell

mongo

1. Show all databases

show dbs

1. Use the `library` database

use library

1. Show all the collections inside the `library` database

show collections

1. Using the insert method Add an author with the name of "John", age of 37

db.authors.insert({name: "John", age: 37})

2. Using the insert method Add another author with the name of "Jane", age of 42 and give her a property of books which is an empty array.

db.authors.insert({name: "Jane", age: 42, books: []})

3. Using the .save() method, find an author with an age greater than or equal to 42 and then change the age to 33. Finally, save that author.

//works but doesnt use save
db.authors.update({age: {$gt:41}},{ $set: {age:33}})

//doesnt work but seems close, throws "canonicalize query error"
db.authors.save(db.authors.findOne({age: {$gte:11}}, {$set: {age:33}}))


1. Find all of the authors

db.authors.find()

1. Find an author with the name of John

db.authors.find({name:"John"})

2. Find all of the authors but limit the search to one

db.authors.find().limit(1)

3. Find an author whose name is not equal to "John" using the `$ne` operator

db.authors.find( {name: { $ne : "John"}})

1. Update an author who has a name of "John" and change his name to "James" (without using the set method)

db.authors.update( { name: "John"}, {name: "James"})

1. Update an author named "James" and using the set operator, set his name back to John and age to 37.

db.authors.update( { name : "James"}, { $set: {name: "John", age: 37 }})

2. Delete an author whose name is "John"

db.authors.remove({name:"John"})

13. Delete all of the authors

db.authors.remove({})

1. Create an author whose name is "John" and has an empty array of books

db.authors.insert({name :"John", books:[]})

2. Update John and Using the `$push` operator add the string "Of Mice and Men" into the books array.

db.authors.update({name:"John"}, { $push: {books: "Of Mice and Men"}})

2. Update John and using the `$push` and `$each` operators add the strings "Grapes of Wrath", "The Pearl", "East of Eden", "50 Shades of Gray" into the books array.

db.authors.update({name:"John"}, { $push: { books: { $each: ["Grapes of Wrath", "The Pearl", "East of Eden", "50 Shades of Gray"]}}})

17. Sorry - John Steinbeck didn't write 50 Shades of Gray, using the `$pull` operator, remove that book from the array.

db.authors.update({name:"John"}, { $pull: {books: "50 Shades of Gray"})

18. Finally, using the `$in` operator, update an author who has a book "Of Mice and Men" and "The Pearl" in the books array and change their name to "John Steinbeck"

db.authors.update( {books : { $in: ["Of Mice and Men", "The Pearl"]}}, {$set : {name:"John Steinbeck"}})





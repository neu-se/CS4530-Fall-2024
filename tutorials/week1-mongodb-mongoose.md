---
layout: page
title: MongoDB and Mongoose
permalink: /tutorials/week1-mongodb-mongoose
parent: Tutorials
nav_order: 4
---
This tutorial provides basic introduction to MondoDB and Mondoose

Contents:
* [MongoDB Concepts](#mongodb-concepts)
* [Mongoose representation of MongoDB Concepts](#mongoose-representation-of-mongodb-concepts)
* [Databases, Collections, and Documents](#databases-collections-and-documents)
* [ObjectIDs and References](#objectids-and-references)
* [Queries](#queries)
* [Examples](#examples)
* [Resources](#resources)


# A mini-tutorial on MongoDB and Mongoose

## MongoDB Concepts

- An _installation_ consists of a set of named _databases_.
- A _database_ consists of a set of named _collections_.
- A _collection_ consists of a set of _documents_.
- A _document_ is a set of (property,value) pairs.
- A _schema_ is a set of (property,type) pairs. All of the documents in a single collection should satisfy the same _schema_.

## Mongoose representation of MongoDB Concepts

### Databases, Collections, and Documents

Mongoose provides representations of MongoDB concepts in the TypeScript/JavaScript language.

- In any given program `mongoose` refers to a particular database in a particular MongoDB instance. For example, executing

```typescript
await mongoose.connect("mongodb://127.0.0.1:27017/pets");
```

causes mongoose to refer to the `pets` database in the local MongoDB instance.

- A MongoDB schema is represented in Mongoose by an object of class `mongoose.Schema`.
  For example, executing

```typescript
const kittySchema = new mongoose.Schema({
  name: String,
  color: String,
});
```

causes `kittySchema` to represent a Mongo schema with a single property, `name`, of type `String`.

References to other documents are represented by properties with type `Types.ObjectID` (more on this later)

In this document, we will use the terms 'property' and 'field' interchangeably.

- A MongoDB collection of documents
  is represented in Mongoose by a TypeScript constructor created by `mongoose.model`. For example

```typescript
const Kitten = mongoose.model("Kitten", kittySchema);
```

causes `Kitten` to refer to a collection named 'Kitten' in the current instance; all the documents in the `Kitten` collection should satisfy the schema represented by `kittySchema`.

- A document with schema `M` is represented by a TypeScript object created by saying `new C`, where `C` is constructor created by `mongoose.model`. For example

```typescript
const fluffy = new Kitten({ name: "fluffy", color: "black" });
```

creates a document intended for insertion in the collection named `Kitten`.

- In Mongoose, creation of a document is separate from being inserted in a collection. So to actually insert `fluffy` in the `Kitten` collection, we need to execute

```typescript
await fluffy.save();
```

Note that most of the operations that touch the database are asyncs.

### ObjectIDs and References

In MongoDB, every document has a unique identifier, which is kept in its `_id` field.

### Queries

In Mongoose, a query is a recipe for retrieving documents from a collection. There are **lots** of ways to do this. Here are some that work (for a collection called Dogs)

```typescript
Dog.find(); // finds all documents in the `Dog` collection
Dog.findOne({ name: "Buddy" }); // finds one of the dogs named 'Buddy'
Dog.find({ breed: "Labrador" }); // finds all dogs of the given breed
```

These are all asyncs, so you need to `await` them.

The query syntax offers lots of methods for selecting, sorting, etc. Take a look at this example, which two very different ways of writing the same query:

```typescript
// With a JSON doc
Person.find({
  occupation: /host/,
  "name.last": "Ghost",
  age: { $gt: 17, $lt: 66 },
  likes: { $in: ["vaporizing", "talking"] },
})
  .limit(10)
  .sort({ occupation: -1 })
  .select({ name: 1, occupation: 1 })
  .exec(callback);

// Using query builder
Person.find({ occupation: /host/ })
  .where("name.last")
  .equals("Ghost")
  .where("age")
  .gt(17)
  .lt(66)
  .where("likes")
  .in(["vaporizing", "talking"])
  .limit(10)
  .sort("-occupation")
  .select("name occupation")
  .exec(callback);
```

For small projects like the one in the course, it is probably preferable to
use the simplest Mongoose queries you can, and then process the list of documents that the query returns.

There are some circumstances where it is helpful to the query do more work. Consider, for example, the following excerpt from `models/application.ts`

```typescript
const q = await QuestionModel.findOneAndUpdate(
  { _id: new ObjectId(qid) },
  { $inc: { views: 1 } },
  { new: true }
).populate({ path: "answers", model: AnswerModel });
return q;
```

Here we are give an objectID `qid`. The call to `.findOneAndUpdate` first finds a document whose `_id` field matches `qid`. It then calls the document's `$inc` method to increment its `views` field by 1. The default behavior of `findOneAndUpdate` is to return the original (unmodified) document. But that's not what we wanted here, so we add a third argument `{ new: true }` to return the updated document. All that would be hard to do except by making it part of `findOneAndUpdate`.

### Examples
A simple example (i.e, example.ts) can be accessed [here](./assets/week1-mongodb-mongoose/tutorial.zip). 

### Resources

* [Official Mongoose/TypeScript docs](https://mongoosejs.com/docs/typescript.html)
* [Mongoose Queries](https://mongoosejs.com/docs/queries.html)
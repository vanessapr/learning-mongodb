# Learning Mongo

https://www.youtube.com/watch?v=c2M-rlkkT5o

mongodb://root:example@localhost:27017

```sh
show dbs

use school

db.createCollection("students")

db.dropDatabase()

db.students.insertOne({ name: "SpongeBob", age: 30, gpa: 3.2 })
db.students.find()

db.students.insertMany([{name: "Patrick", age: 30, gpa: 3.0},{name: "Sandy", age: 25, gpa: 3.5}])

db.students.insertOne({
  name: "Larry", age: 32, gpa: 2.8, fullTime: false,
  registerDate: new Date(), gradutionDate: null,
  courses: ["Biology", "Chemistry"],
  address: {street: "123 Fake ST.", city: "Bikini Bottom", zip: 1516}
})

db.students.find().sort({name: 1})
db.students.find().limit(1)

db.students.find({fullTime: false})

db.students.find({}, {_id: false, name: true})

db.students.updateOne({name: "SpongeBob"}, {$set: {fullTime: true}})

db.students.updateOne({_id: ObjectId("66bd128dd2acef87003948eb")}, {$set: {fullTime: false }})

db.students.updateOne({ _id: ObjectId("66bd0ffed2acef87003948e8")}, {$unset: {fullTime: ""}})

db.students.updateMany({}, {$set: {fullTime:false}})
db.students.updateMany({fullTime: {$exists: false}}, {$set:{fullTime: true}})

db.students.deleteOne({name: "Sandy"})
db.students.deleteMany({fullTime: false})
db.students.deleteMany({registerDate:{$exists:false}})

db.students.find({name: {$ne: "SpongeBob"}})
db.students.find({age: {$lte: 30}})
db.students.find({name: {$in: ["Patrick", "Sandy"]}})
db.students.find({$and: [{fullTime: false}, {age: {$gte:22}}]})
db.students.find({$nor: [{fullTime: false}, {age: {$gte:22}}]})
db.students.find({age: {$not: {$lte: 30}}})

db.students.find({name: "Larry"}).explain("executionStats")
db.students.createIndex({name:1})
db.students.getIndexes()
db.students.dropIndex("name_1")

show collections
db.createCollection("teachers", {capped: true, size:10000000, max:100}, {autoIndexId:false})
```

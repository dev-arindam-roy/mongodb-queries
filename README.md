# MongoDB Queries
A collection of mondodb queries

## Some Notes

```
1) First install mongodb community server [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
2) Second extract the mongo shell .zip file and paste into the C: drive [https://www.mongodb.com/try/download/shell](https://www.mongodb.com/try/download/shell)
3) Create 2 system env path variable
Like:
C:\Program Files\MongoDB\Server\6.0\bin
C:\mongosh\mongosh-1.8.0-win32-x64\mongosh-1.8.0-win32-x64\bin

4) Open CMD and run 'mongod' command. 
5) Open CMD and run 'mongosh' command.

if both command running successfully then installation is correct and completed.

=> we will be use the mongo shell (mongosh) to query execution
=> casesensitive
```

## Query Documentation
[https://www.mongodb.com/docs/manual/tutorial/query-documents/](https://www.mongodb.com/docs/manual/tutorial/query-documents/)

```javascript
1)  mongod --version
2)  show dbs // if any db don't have any collection then it will not shown
3)  use [database-name] // create a new database if not exist else use it 
4)  db.createCollection("[collection-name]")
5)  show collections
6)  db.users.insertOne({"first_name":"Arindam", "last_name": "Roy"})
7)  db.users.find() || db.users.find().pretty() || db.users.find({}) 
8)  db.users.updateOne({"first_name":"Arindam"}, {$set:{"last_name":"Dutta"}})
9)  db.users.drop()
10) db.dropDatabase()
11) db.users.insertMany([{"id":9, "name":"Demo user9", "age":25}, {"id":10, "name":"Demo user10", "age":22}, {"id":11,"name":"Demo user10","age":20}])
12) db.users.insertOne({"id":20,"name":"Demo user20","age":18,"language":["php","asp","jsp"], "reg_date": new Date('2024-01-15'), "address":{"city":"kolkata","pincode":"700150","state":"WB","landmark":"JS Club"},"country":"IND"})
13) db.users.find().sort({"id":1}) //sort by id asc
14) db.users.find().sort({"id":-1}) //sort by id desc
15) db.users.find().sort({"name":-1})
16) db.users.find().sort({"age":1})
17) db.users.find().sort({"age":-1})
18) db.users.find().limit(1) // return 1 document
19) db.users.find().limit(3) // return 3 documents
20) db.users.find().sort({"age":-1}).limit(3) // return 3 documents desending order of age
21) db.users.find({age:35}) // find users who have age = 35
22) db.users.find({name:"Demo user10"}) // find user whose name is "Demo user10"
23) db.users.find({name:"Demo user10", age:20}) // find user whose name is "Demo user10" and age = 20
24) db.users.find({},{name:true}) // get all records/documents from users collection but show only name and document object id (document object id by default print)
25) db.users.find({},{_id:false,name:true}) // get all records/documents from users collection but show only name (as document object id is false)
26) db.users.find({},{_id:false,name:true,age:true}) // get all records/documents from users collection but show only name and age
27) db.users.find({_id: ObjectId("65d7913265c441475d658274")}) // find user by document object id (default primary key)
28) db.users.updateOne({_id: ObjectId("65d7913265c441475d658274")}, {$set:{id:88, "name":"Demo user88", age:88}}) // update an user by document object id
29) db.users.updateOne({_id: ObjectId("65d7913265c441475d658274")}, {$set:{address:{"city":"kolkata","state":"WB","pincode":"700123"}}}) // also can update with new parameters like here the 'address'. Previously the 'address' was not present for this user. That's means we can update any exist information and as well as we can add we information within a document.
30)  db.users.updateOne({_id: ObjectId("65d7913265c441475d658274")}, {$unset:{address:"",age:""}}) // we can remove a field or parameter from a document. Here we have removed the 'address' and 'age' field/parameter from this user document
31) db.users.updateMany({}, {$set:{address:{"city":"kolkata","state":"WB","pincode":"700444"}, "country":"IND"}}) // Update all documents with 'address' and 'country' parameters as we don't pass any filter key (in the first argument)
32) db.users.updateMany({"reg_date":{$exists:false}}, {$set:{"reg_date":new Date().toDateString()}}) // Those who don't have the 'reg_date' field/parameter only those are updated with the parameter 'reg_date'
33) db.users.updateMany({"language":{$exists:false}}, {$set:{"language":["node js","mongodb"]}}) // same the above
34) db.users.deleteOne({name:"Demo user10"})
35) db.users.deleteOne({name:"Demo user10", age:22}) // delete a document where name = 'Demo user10' and age = 22
36) db.users.deleteMany({country:"IND"}) // delete all documents where country = 'IND'
37) db.users.deleteMany({"reg_date":{$exists:false}}) // delete all documents which don't have the 'reg_date' parameter
38) db.users.find({name:"user5"},{_id:false,location:true}) // find by name = 'user5' and show only 'location'
39) db.users.find({name:"user5"},{_id:false,location:true,name:true,company:true}) // find by name = 'user5' and show only 'location,company,company'
40) db.users.updateOne({name:"user5"}, {$unset:{location:""}})	// find by name = 'user5' and removed the parameter 'location' for one document
41) db.users.updateMany({name:"user5"}, {$set:{company:"TCS"}})
42) db.users.find({location:{$exists:false}}) // find user document whose don't have the 'location' parameter
43) db.users.find({location:{$exists:false},age:22}) // find user document whose don't have the 'location' parameter and 'age' = 22
44) db.users.deleteMany({company:"TCS"}) // delete all documents where company = 'TCS'
45) db.users.find({age:{$ne:20}}) // find all users document where age != 20
46) db.users.find({age:{$lt:22}}) // find all users document where age < 22
47) db.users.find({age:{$lte:22}}) // find all users document where age <= 22
48) db.users.find({age:{$gt:22}}) // find all users document where age > 22
49) db.users.find({age:{$gte:22}}) // find all users document where age >= 22
50) db.users.find({age:{$gte:22, $lte:25}}) // find all users document where age >= 22 and age <=25
51) db.users.find({age:{$gt:22, $lte:25}}) // find all users document where age > 22 and age <=25
52) db.users.find({age:{$gt:22, $lt:25}}) // find all users document where age > 22 and age < 25
53) db.users.find({name:{$in:["user1","user2","user5"]}}) // find all users document where name in the array ["user1","user2","user5"]
54) db.users.find({name:{$nin:["user1","user2","user5"]}}) // find all users document where name not in the array ["user1","user2","user5"]
55) db.users.find({$and: [{id:{$gt:3}},{age:{$gte:20, $lt:25}}]}) // find all users document where id > 3 and (age >=20 && age < 25)
56) db.users.find({$and: [{age:{$gte:21}},{age:{$lte:23}}]}) // find all users document where age >= 21 and age <= 23
57) db.users.find({$or: [{name:"user6"},{age:{$lte:20}}]}) // find all users document where name = 'user6' or age <= 20
58) db.users.find({$nor: [{name:"user6"},{age:{$lte:20}}]}) // find all users document where name != 'user6' and age not <= 20
59) db.users.find({age:{$not:{$gte:22}}}) // find all users document where age not >= 22
60) db.users.find({age:{$not:{$gte:21, $lte:24}}}) // find all users document where age (not (>= 21 and <=24))
61) db.users.find({name:"user3"}).explain("executionStats") // to check a query execution details (default followed liniear search)
62) db.users.createIndex({name:1}) // create index
63) db.users.getIndexes() // show indexes
64) db.users.dropIndex("name_1") // drop index (index name will get from getIndexes())
65) db.createCollection("students", {capped:true, size:1000000000, max:5}, {autoIndexId:false})
66) db.createCollection("students", {capped:true, size:1000000000, max:5}, {autoIndexId:true})
67) db.users.find().count()
68) db.users.createIndex({location: 'text'}) // called 'text index'. Here we have created a text index for the 'location' field
69) db.users.find({$text:{$search:"kolkata"}}) // text search in users document where text index have applied
70) db.users.find({age:{$mod:[2,1]}}) // get all users documents where age devided by 2 and reminder will be 1
71) db.users.find({age:{$mod:[2,0]}}) // get all users documents where age devided by 2 and reminder will be 0
72) db.users.find({age:{$mod:[2,0]}}).count()


A example users collection
==============================
[
  {
    _id: ObjectId("65dc4a0403b8c1bb5d76e7ef"),
    id: 300,
    name: 'user300',
    lang: [ 'Eng', 'Ben', 'Hin' ],
    company: [ { name: 'TCS', salary: 50000 } ]
  },
  {
    _id: ObjectId("65dc4a2a03b8c1bb5d76e7f0"),
    id: 400,
    name: 'user400',
    lang: [ 'Eng', 'Den', 'Fr' ],
    company: [ { name: 'CTS', salary: 70000 } ]
  }
]

73) db.users.find({"lang":"Eng"}) // find by 'lang'. Mongo can find value within the array field.
74) db.users.find({"lang":"Den"}) // we don't need to pass any array, just pass the value that exist/avaliable in array
75) db.users.find({"company.name":"TCS"}) // also we can find by object value
76) db.users.find({"company.name":"TCS"}).count() // return count
77) db.users.find({"company.name":"TCS"}).size() // return count

[
  {
    _id: ObjectId("65dc4a0403b8c1bb5d76e7ef"),
    id: 300,
    name: 'user300',
    lang: [ 'Eng', 'Ben', 'Hin' ],
    company: [
      { name: 'IBM', salary: 100000 },
      { name: 'CISPL', salary: 8900000 }
    ]
  },
  {
    _id: ObjectId("65dc4a2a03b8c1bb5d76e7f0"),
    id: 400,
    name: 'user400',
    lang: [ 'Eng', 'Den', 'Fr' ],
    company: [ { name: 'CTS', salary: 70000 } ]
  }
]

78) db.users.find({"lang":{$size:3}}) // get those user document who know atleast 3 languages. here 'lang' is an array
79) db.users.find({"company":{$size:2}}) // same thing apply on the object. here 'company' is a collection of objects
80) db.users.find({lang:{$all:["Eng","Den"]}}) // find multiple value within an array. here who knows "Eng" and "Den"
81) db.users.find({lang:{$in:["Eng","Den"]}}) //  find multiple value within an array. here who knows "Eng" or "Den"

[
  {
    _id: ObjectId("65dc5d9b03b8c1bb5d76e7f1"),
    id: 1,
    products: [
      { name: 'apple', qty: 10 },
      { name: 'boat', qty: 12 },
      { name: 'mi', qty: 10 }
    ]
  },
  {
    _id: ObjectId("65dc5dbd03b8c1bb5d76e7f2"),
    id: 1,
    products: [
      { name: 'apple', qty: 18 },
      { name: 'realme', qty: 5 },
      { name: 'samsung', qty: 12 }
    ]
  },
  {
    _id: ObjectId("65dc5dc803b8c1bb5d76e7f3"),
    id: 1,
    products: [
      { name: 'apple', qty: 3 },
      { name: 'realme', qty: 15 },
      { name: 'samsung', qty: 22 }
    ]
  }
]

82) db.cart.find({"products":{$elemMatch:{"name":"apple","qty":{$gt:10}}}}) // exact object element match.  
83) db.cart.find({"products":{$elemMatch:{"name":"apple","qty":{$gte:10}}}}) // same above. find those documents where array of the product's collection have name = 'apple' and qty >= 10
84) db.cart.find({"products":{$elemMatch:{"name":"mi","qty":{$gte:10}}}})

85) db.users.find().sort({name:1, age:-1})
86) db.users.find().sort({name:1, age:-1}).skip(20)
87) db.users.find().sort({name:1, age:-1}).limit(10)
88) db.users.find().sort({name:1, age:-1}).count()
89) db.users.find().sort({name:1, age:-1}).size()
90) db.users.find().sort({name:1, age:-1}).skip(5).limit(20)

91) db.users.findOne()
92) db.users.updateMany({}, {$inc:{id:1000}}) // increment id by 1000
93) db.users.updateOne({id:1007}, {$max:{age:50}}) // update 1007 user age upto or maximum 50 (if the current age is less than 50)
94) db.users.updateOne({id:1007}, {$min:{age:10}}) // update 1007 user age upto or minimum 10 (if the current age is grater than 10)
95) db.users.updateMany({name:"user6"}, {$min:{age:12}})
96) db.users.updateMany({name:"user6"}, {$mul:{age:2}}) // multiply user age by 2
97) db.users.updateMany({}, {$rename:{age:"user_age"}}) // rename a document parameter/field. here we have renamed the 'age' field by 'user_age'

```

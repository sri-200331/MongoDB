 mongodb -mongodb.md

 comparison operatores:
     >                $gt
     >=               $gte
     <                $lt
     <=               $lte
     =                $eq
     !=               $ne
     value in array   $in
     not in array     $nin

find
findOne
findId

10/12/25

logical operator
     and     $and
     or      $or

update doc
     updateOne()
     updateMany()
     
     +  $set


     findOneAndupdate()
     findAndupdate()


<!-- Mongoose queries
       1.findById()
       2.findByIdAndUpdate()
       3.findByAndDelete -->



task:delete
         deleteOne
         deleteMany



 Regex
          $regex

        1.$regex:'A'  (namba caps pota caps eduthutu varum('A') and small pota small eduthutu varum('a'))  - db.products.find({productName:{$regex:'c'}})

        2.$regex:'^A' (starting with A)   -  db.products.find({category:{$regex:'^g'}})

        3.$regex:'A$' (ending with A)      -  db.products.find({productName:{$regex:'s$'}})

        4.$regex:'A'{$options:'i'}  (case sensitive-small and caps ethuva irunthalum eduthutu varum )    - 
        
                                                     db.products.find({productName:{$regex:'r',$options:'i'}})




11/12/25

Aggregate -operations
    
    $match-(similar to find operation)
    $group
    $sum
    $sort-(descending)
    $project















use schoolDB
show collections
<!-- add data -->
db.students.insertOne({name:'thia',age:6,city:'pnk'})

db.students.insertMany([
  {name:'thanvi',age:2,city:'pnk'},{name:'adhi',age:23,city:'pnk'}])
show collections

<!-- fetch data-->
db.students.find()
db.students.find().pretty()  

<!-- conditional operators -->
db.students.find({age:{$gt:22}})

<!-- Logical operator -->
1.db.students.find({
  $and:[{age:23},{city:'chennai'}]
  })

2.db.students.find({
  $or:[{age:{$gt:22}},{city:'chennai'}]
})

<!-- update and set -->
db.students.updateOne({name:kavya B},{$set:{city:'trichy'}})
db.students.find()

db.students.updateMany({city:'chennai'},{$set:{city:'trichy'}})
db.students.find()

<!-- aggregate -->
<!--1. $match -->
db.students.aggregate([
    {$match:{age:23}
    }])

<!-- 2.$groupand $sum -->
 db.students.aggregate([
  {$match:{city:'chennai'}},
  {$group:{_id:'$age',total:{$sum:1}}}])

  <!-- 3.$sort -->
  












  <!-- task -store -->

  MongoDB Task - Comparison Operators 
A small supermarket wants to store product details in MongoDB to simplify billing and stock checking. They ask you to create a database called storeDB and a collection named products. The manager gives you five product details including product name, price, and category, and wants them inserted using insertMany. After insertion, they want to check whether the data is stored correctly by displaying all products. Next, the manager asks you to find the product whose price is exactly 100. They also want to list products that are not in the “Snacks” category. Later, they request all products priced greater than 50, followed by products priced less than 40. Finally, the manager wants to view products whose category is either “Grocery” or “Beverages”. Perform all the required MongoDB queries.

 Questions to Answer (Based on the Above Paragraph)
1.Create storeDB and the products collection.
          use storeDb

2.Insert the 5 products using insertMany().
      db.products.insertMany([
         {productName:'milk',price:40,category:'grocery'},
         {productName:'chips',price:20,category:'snacks'},
         {productName:'coffee',price:120,category:'beverages'},
         {productName:'rice',price:100,category:'grocery'},
         {productName:'juice',price:60,category:'beverages'}
  ])


3.Display all products.
       db.products.find()


4.Find the product with price = 100 using $eq.
       db.products.find({price:{$eq:100}})


5.List all products not in category “Snacks” using $ne.
       db.products.find({category:{$ne:'snacks'}})
      

6.Find products with price > 50 using $gt.
        db.products.find({price:{$gt:50}})


7.Find products with price < 40 using $lt.
         db.products.find({price:{$lt:40}})


8.Find all products whose category is Grocery or Beverages using $in
          db.products.find({category:{$in:['grocery','beverages']}})









1. Write a query to insert a user with name, email, and age into a users collection. 
  db.users.insertMany([
  {name:'Poomani',age:23,email:'poomanibharathi11@gamil.com'},
  {name:'Bharathi',age:22,email:'bharathi11@gamil.com'},
  {name:'Mani',age:17,email:'mani@gmail.com'},
  {name:'boomi',age:20,eamil:'boomi@gmail.com'}
   ])
   
  db.users.find()


2. Write a query to find users whose age is between 20 and 30. 
    db.users.find({
        age:{$gte:20,$lte:30}
     })


3. Write a query to update a user's age to 30 using their name. 
    db.users.updateOne(
      {name:'boomi'},{$set:{age:30}}
    )
    db.users.find()


4. Write a query to delete users whose age is less than 18. 
    db.users.find({age:{$lt:18}})



5. Write a query to count the total number of users in the collection.
      db.users.countDocuments()






1. Write a query to insert a new user document in a users collection.
      db.users.insertMany([
         {name:'Poomani',age:23,email:'poomanibharathi11@gamil.com'},
         {name:'Bharathi',age:22,email:'bharathi11@gamil.com'},
         {name:'Mani',age:17,email:'mani@gmail.com'},
         {name:'boomi',age:20,eamil:'boomi@gmail.com'}
      ])
   
      db.users.find()

      db.users.insertOne({
         name:'nithya',age:27,email:'nithya2@gamil.com'
      })
 

2. Write a query to find all users whose age is greater than 25.
      db.users.find({
         age:{$gt:25}
      })


3. Write a query to update a user's email using _id. 

4. Write a query to delete a user by name. 
5. What is the difference between SQL and MongoDB?



1.group and count
 db.users.aggregate([
  {$group:{_id:"$age", total:{$sum:1}}}
])

2. find average age
db.users.aggregate([
  {$group:{_id:null, avgAge:{$avg:"$age"}}}
])


3. match condition
db.users.aggregate([
  {$match:{age:{$gt:25}}}
])




1. What is MongoDB?

MongoDB is a NoSQL database that stores data in JSON-like documents (BSON format) instead of tables and rows.


2. What is a Collection in MongoDB?

A collection is similar to a table in SQL.

It stores multiple documents.


3. What is a Document?

A document is a single record in MongoDB stored in JSON format.


4. What is BSON?

BSON (Binary JSON) is the format MongoDB uses to store documents.

It supports additional data types like:

Date

Binary

ObjectId

5. What is ObjectId?

ObjectId is the unique identifier automatically created for each document.

Example:

"_id": ObjectId("65f3a0d9f2d1a4")
6. Difference Between SQL and MongoDB
SQL	MongoDB
Table	Collection
Row	Document
Column	Field
Fixed schema	Flexible schema
7. What is Index in MongoDB?

An Index improves the search performance of queries.

Example:

db.users.createIndex({name:1})

Now searching by name will be faster.

8. What is Aggregation?

Aggregation is used to process data and return calculated results.

Example operations:

sum

average

group

filter

Example:

db.orders.aggregate([
  {$group:{_id:"$product", total:{$sum:"$price"}}}
])
9. What is Replication?

Replication means copying data across multiple servers to increase availability and reliability.

10. What is Sharding?

Sharding means splitting large data into multiple servers for better performance.
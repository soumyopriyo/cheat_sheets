-NoSQL-Non-sutuctured Databases--the data is not constricted to the shape of a table linke in a relational db.
-Mongo DB stores binary representation of JSON data kown as BSON.

-Collection(in NoSQL)=Tables(in SQL)

-Documents(in NoSQL)=Rows(in SQL)

-inside the documents we have key:value pairs.
ex.
{
firstname:"john"
latname:"miller"
.
.
.
}

->delete db
***********
we need to be inside the db that we want ot delete.
db.dropDatabase()

create collections
*******************
db.createCollection('collection_name')



sample data
*************
{
	first_name:"john",
	last_name:"miller",
	memberships:["mem1","mem2"], //arrays
	address:{			/**
		 street:"12th st",	*
		 city:"Bangalore"	* Objects
	}				*/
	contacts:[
		{name:"jerry",relationship:"brother"}//arrays of objects
	]
}
create user
**************
db.createUser({
	user:"john",
	pwd:"123",
	roles:["readWrite","dbAdmin"]
});

create collections
********************
db.createCollection('customers');

insert one row
***************
db.customer.insertOne(
{
name:"john",
age:21,
status:"A",
date:new Date(),
groups:["editor","manager",]
})

insert multiple rows   ------array of objects
*********************
db.customer.insertMany(
[{
name:"john",
age:21,
status:"A",
groups:["editor","manager",]
},
{
name:"jerry",
age:21,
status:"A",
email:"jerry@gmail.com",
groups:"CEO"
},
{
name:"ram",
age:21,
status:"A",
groups:["student","salesman"]
}
])


querying data
***************
--->db.users.find()---select * from users(tablename).

	editing the documents in the collections
	************************
	db.users.insertOne(
	{
	name:"john",
	age:21,
	status:"A",
	email:"john@gmail.com",
	groups:["editor","manager",]
	}
	)
---->db.users.find({name:"john"})---select * from users where name="Soumyopriyo";

----->db.customer.find({name:"john"}).limit().count()---it will count only the rows that are being printed with the name=soumyopriyo.

----->db.customer.find().sort(member:1)------it will sort every rows/documents with member in ascending order.

----->db.customer.find().sort(member:-1)------it will sort every rows/documents with member in descending order.


update documents/rows
**********************

db.customer.update({name:"jerry"},
{
$set:{
name:"jerry",
age:18,
status:"A",
email:"jerry.com",
groups:"CEO"
}
}
)

increment operator
******************
//here we will use the increment operator
db.customer.update({name:"jerry"},
{
$inc:{age:1}
}
)

rename operator
*****************
db.customer.update({name:"jerry"},
{
$rename:{age:'points'}
}
)

delete operator
*****************
db.customer.remove({_id: ObjectId("6146e7e525e33eb9f2a2130e")})

embedding comments suppose in a blog post
********************************************
db.customer.update({name:"rony"},
{
$set:{
comments:[
{user:"Mary",
body:"Comment One",
date:new Date()},
{
user:"john",
body:"Comment TWO",
date:new Date()
}
]
}
}
)

to find a certain elements
***************************
db.customer.find({
comments:{
$elemMatch:{user:"Mary"}
}
})
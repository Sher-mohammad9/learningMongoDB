# MongoDB

### Create Database

Mongodb me 'USE' command ka use database create karane or  database ko use karane ke liye kiya jata hai.

Syntax :
```sql
use Database_Name;
```

Example :
```sql
use WecodeAcademy;
```

### Create collection 

db.createCollection("Collection_Name") MongoDB mein ek command hai jo ek nayi collection ko database mein create karne ke liye use kiya jata hai. Is command ke dwara aap kisi bhi database mein ek nayi collection bana sakte hain. Collection_Name ki jagah aap apne collection ka naam de sakte hain. Agar is naam se koi collection pehle se hi maujood hai toh yeh command us collection ko fir se create nahi karega. Yeh command ek JSON object mein ek khaali collection ko return karta hai.

Syntax :
```sql
db.createCollection("Collection_Name");
```

Example :
```sql
db.createCollection("student");
```

### Insert data in database

- db.collection_name.insertOne() 

db.collection_name.insertOne() MongoDB mein ek command hai jo ek naye document ko collection mein insert karne ke liye use kiya jata hai. Yeh command ek hi document ko insert karta hai, aur usey JSON format mein accept karta hai. Jab yeh command execute hoti hai, toh ek unique identifier field, 'id' automatically document mein generate hoti hai.

Syntax :
```sql
db.collection_name.insertOne({add_Data});
```

Example :
```sql
db.student.insertOne({"name" : "Sher mohammad", "mobile" : 9610406098, "email_address" : "shermo2453@gmail.com", "address" : "Nagour, Merta city"})
```

- db.collection_name.insertMany() 

db.collection_name.insertMany() MongoDB mein ek command hai jo ek naye document ko collection mein insert karne ke liye use kiya jata hai. Yeh command ek ya ek se jyada document ko insert karta hai, aur usey JSON format mein accept karta hai. Jab yeh command execute hoti hai, toh ek unique identifier field, 'id' automatically document mein generate hoti hai.

Syntax :
```sql
db.collection_name.insertMany([{add_Data}]);
```

Example :
```sql
db.student.insertMany([{"name" : "Sher mohammad", "mobile" : 9610406098, "email_address" : "shermo2453@gmail.com", "address" : "Nagaur, Merta city"}, 
{"name" : "mohammad Hassan", "mobile" : 9854543543, "email_address" : "Hassan24@gmail.com", "address" : "Jhotwara, jaipur"},
{"name" : "Rakesh", "mobile" : 5754646456, "email_address" : "Rakesh53@gmail.com", "address" : "Nagour, Peeh"},
]);
```

### Select data from database

- db.collection_Name.find()

db.collection_Name.find() MongoDB mein ek command hai jo ek collection se ek ya ek se jyada documents ko get karne ke liye use hoti hai. Is command ka use ek collection mein ek ya adhik documents ko get karne ke liye kiya jata hai. Yeh command ek cursor ko return karta hai, jisme documents array me store hote hain. Ham is cursor ko hasNext() aur next() methods ka use karke documents ko access kar sakte hain. Yah command documents ko JSON format mein return karta hai.

Syntax :
```sql
db.collection_Name.find();  
```

Example :
```sql
db.student.find();
```

- db.collection_Name.findOne()

MongoDB mein ek command hai jo collection se ek document ko get karne ke liye use kiya jata hai. Is command ka use collection mein ek document ko get karne ke liye kiya jata hai. Yeh command ek hi document ko get karta hai, aur usey JSON format mein return karta hai.

Syntax :
```sql
db.collection_Name.findOne();  
```

Example :
```sql
db.student.findOne({querie});
```

### Update data in database

- db.collection_Name.updateOne({querie},{$set : {querie}});


MongoDB mein db.collection_Name.updateOne() command ka use ek collection me ek document ko update karane ke liye hota hai.
1.Ek query object jisme hum woh document identify karte hain jisko hum update karna chahte hain.
2.Ek update object jisme hum woh changes bataate hain jo hum uss document mein karna chahte hain.

Syntax :
```sql
db.collection_Name.updateOne({querie},{$set : {querie}});
```

Example :
```sql
db.student.updateOne({"Role No." : 10}, {$set : {"mobile" : 9845335458}});
```

- db.student.updateMany({querie}, {querie});

MongoDB mein db.collection_Name.updateMany() command ka use ek collection me ek ya ek se jyada  document ko update karane ke liye hota hai.
1.Ek query object jisme hum woh document identify karte hain jisko hum update karna chahte hain.
2.Ek update object jisme hum woh changes bataate hain jo hum uss document mein karna chahte hain.

Syntax :
```sql
db.collection_Name.updateMany({querie},{$set : {querie}});
```

Example :
```sql
db.student.updateMany({"studentName" : {$in : ["Raja", "Akash"]}}, {$set : {"mobile" : 9845335458}});
```

### delete data in database

- db.collection_name.deleteOne({querie});

mongodb mein "db.collection_name.deleteOne()" command ka use database mein ek document ko delete karne ke liye kiya jata hai. Yeh command ek hi document ko delete karta hai.

Syntax :
```sql
db.student.deleteOne({querie});
```

Example :
```sql
db.student.deleteOne({"studentName" : "Sher Mohammad"});
```

- db.collection_name.deleteMany({querie}, {querie});

mongodb mein "db.collection_name.deleteMany()" command ka use database mein ek ya ek se jyada document ko delete karne ke liye kiya jata hai. Yeh command ek ya ek se jyada document ko delete karta hai.

Syntax :
```sql
db.student.deleteMany({querie});
```

Example :
```sql
db.student.deleteMany({"studentName" : "Sher Mohammad"});
```


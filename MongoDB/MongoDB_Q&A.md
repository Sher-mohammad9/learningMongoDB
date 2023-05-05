# Question & Answer

### 1. Vo sare students ki list btao jinka email ni hai 

```nosql
db.student.find({"email" : null});
```

### 2. Vo sare students ki list btao jinka mobile number same hai 

```nosql
db.student.aggregate(
[
  {
  $group : {_id:"$mobile", 
             sameMobileNo:{
             	$push:"$$ROOT"
             }
           }
  }
]
)
```

### 3. Sare students ka only email and mobile return krvao

```nosql
db.student.find({}, {"email" : 1, "mobile" : 1});
```

### 4. students record ki name se sorting krni hai 

- Sort ascending.

```nosql
db.student.aggregate([{$sort : {"studentName" : 1}}]);
```

- Sort descending.

```nosql
db.student.aggregate([{$sort : {"studentName" : -1}}]);
```

### 5. vo sare students ki list return kro jinka admission last 3 months me hua hai 

```nosql
```

### 6. vo sare students ka only naam btao jinka admission current month me hua hai 

```nosql
```

### 7. vo sare students ka naam btao jinki dob year same hai 

```nosql
db.student.aggregate(
[
  {
  	$group : {_id:"$dob", 
  	studentName:{
  		$push: "$studentName"
  	}
  }
  }
]
)
```

### 8. vo sare students ka naam btao jinka address jaipur, nagaur ya karauli ho 

```nosql
db.student.find({"address" : {$in : ["jaipur", "nagaur", "karauli"]}});
```

### 9. vo sare students ka naam btao jo Sikar, Jhunjhun se ni hai 

```nosql
db.student.find({"address" : {$nin : ["sikar", "jhunjhun"]}});
```

### 10. vo sare students ka naam btao jinka Address Sikar hai and fathername Rahim hai 

```nosql
db.student.find({$and : [{"address" : "siker"}, {"fatherName" : "rahim"}]}, {"studentName" : 1});
```

### 11. vo sare students ka naam btao jinka fathername Khalil ho or email id rahim@gmail.com ho 

```nosql
db.student.find({$or : [{"studentName" : "khalil"}, {"email" : "rahim@gmail.com"}]}, {"studentName" : 1});
```

### 12. question 11 ko nor se kro 

```nosql
db.student.find({$nor : [{"studentName" : "khalil"}, {"email" : "rahim@gmail.com"}]}, {"studentName" : 1});
```

### 13. Vo sare students ka naam btao jinka father name Ahmed ni hai 

```nosql
db.student.find({"fathername" : {$nin : ["ahmed"]}}, {"studentName" : 1})
```

### 14. Vo sare students ka naam btao jinka mobile 945345435 ni hai

```nosql
db.student.find({"mobile" : {$nin : [945345435]}}, {"studentName" : 1})
```
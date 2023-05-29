# Question & Answer

### 1. Vo sare students ki list btao jinka email ni hai 

```sql
db.student.find({"email" : null});
```

### 2. Vo sare students ki list btao jinka mobile number same hai 

```sql
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

```sql
db.student.find({}, {"email" : 1, "mobile" : 1});
```

### 4. students record ki name se sorting krni hai 

- Sort ascending.

```sql
db.student.aggregate([{$sort : {"studentName" : 1}}]);
```

- Sort descending.

```sql
db.student.aggregate([{$sort : {"studentName" : -1}}]);
```

### 5. vo sare students ki list return kro jinka admission last 3 months me hua hai 

```sql
var currentDate = new Date();
var last3Month = new Date();
last3Month.setMonth(currentDate.getMonth() - 3)

db.student.find({admissionDate : {$gte : last3Month, $lte : currentDate}})
```

### 6. vo sare students ka only naam btao jinka admission current month me hua hai 

```sql
var currentDate = new Date();
var stratMonth = new Date(currentDate.getFullYear(), currentDate.getMonth(), 1);
var endMonth = new Date(currentDate,getFullYear(), currentDate.getMonth() + 1, 0);

db.student.find({admissionDate : {$gte : stratMonth, $lte : endMonth}}, {studentName : 1})
```

### 7. vo sare students ka naam btao jinki dob year same hai 

```sql
```

### 8. vo sare students ka naam btao jinka address jaipur, nagaur ya karauli ho 

```sql
db.student.find({"address" : {$in : ["jaipur", "nagaur", "karauli"]}});
```

### 9. vo sare students ka naam btao jo Sikar, Jhunjhun se ni hai 

```sql
db.student.find({"address" : {$nin : ["sikar", "jhunjhun"]}});
```

### 10. vo sare students ka naam btao jinka Address Sikar hai and fathername Rahim hai 

```sql
db.student.find({$and : [{"address" : "siker"}, {"fatherName" : "rahim"}]}, {"studentName" : 1});
```

### 11. vo sare students ka naam btao jinka fathername Khalil ho or email id rahim@gmail.com ho 

```sql
db.student.find({$or : [{"studentName" : "khalil"}, {"email" : "rahim@gmail.com"}]}, {"studentName" : 1});
```

### 12. question 11 ko nor se kro 

```sql
db.student.find({$nor : [{"studentName" : "khalil"}, {"email" : "rahim@gmail.com"}]}, {"studentName" : 1});
```

### 13. Vo sare students ka naam btao jinka father name Ahmed ni hai 

```sql
db.student.find({"fathername" : {$nin : ["ahmed"]}}, {"studentName" : 1})
```

### 14. Vo sare students ka naam btao jinka mobile 945345435 ni hai

```sql
db.student.find({"mobile" : {$nin : [945345435]}}, {"studentName" : 1});
```

# Test 2

### Q1. Create database wecodeacademy

```sql
use WecodeAcademy;
```

### Q2. create collection batches

```sql
db.createCollection("batches");
```

### Q3. add 5 documents in this way

```sql 
db.batches.insertMany([
  {batchName : "Node.js", student : ["arif", "sher mohammad", "khalil"], duration : 5, fees: 5000, marks : [10,20,30,40,50]}
  {batchName : "Design", student : ["arif", "khalil", "irfan", "adil"], duration : 5, fees: 12000, marks : [10,20,30]}, 
  {batchName : "Java", student : ["arif", "khalil", "irfan"], duration : 5, fees: 13000, marks : [10,80,60]}, 
  {batchName : "javaScript", student : ["arif", "khalil","adil"], duration : 5, fees: 5000, marks : [71,26,99,67]}, 
  {batchName : "ComputerScience", student : ["khalil", "irfan", "adil"], duration : 5, fees: 1000, marks : [60,60,60]}])
```

### Q4. Vo sare batches ke naam btao jinke student ke marks 50% se kam hai
 ```sql
db.batches.find({marks : {$lt : 50}},{batchName : 1, _id : 0});
 ```

### Q5. marks array me se sirf vhi marks rkhne hain jo 60+= hain. baki sbko remove krdo

```sql
db.batches.updateMany({},{$pullAll : {marks : {$lt : 60}}});
```

### Q6. marks array me starting se 3rd index se 5 new marks add krne hai 

```sql
db.batches.updateMany({}, {$push : {marks : {$each : [10,20,30,40,50], $position: 3}}});
```

### Q7. Back/Last se 4th position se 5 new marks add krne hain.

```sql
db.batches.updateMany({}, {$push : {marks : {$each : [70,80,90,100,110], $position: -4}}});
```

### Q8. Students array ko ascending and marks Array ko desc order me sort krna hai 

```sql
db.batches.updateMany({}, {$push : {student : {$each : [], $sort : 1}, marks:{$each : [], $sort : -1}}});
```

### Q9. Marks array me sirf 10 numbers rkhne hain starting se baki sb remove kr dene hain

```sql
db.batches.updateMany({}, {$push : {marks : {$each : [], $slice : 10}}});
```
### Q10. Agar marks array me max number 99 hai to thik otherwise max number 99 krdo

```sql
```

### Q11. fees field ko rename krke totalfees krdo 

```sql
db.batches.updateMany({}, {$rename : {"fees": "totalFee"}});
```

### Q12. duration ko 2 se multiply krdo 

```sql
db.batches.updateMany({}, {$mul : {duration : 2}});
```

### Q13. students array me se Irfan, Adil ka naam hai to remove krdo

```sql
db.batches.updateMany({}, {$pullAll : {student : {$in : ["irfan", "adil"]}}});
```

### Q14. Agar fees 10000 se jyada hai to duration field ko remove krdo

```sql
db.batches.updateMany({totalFee : {$gt : 10000}}, {$unset : {duration : ""}});
```

### Q15. Vo sare students search kro jinke naam me Khan hai aur batchName Designing hai aur fees 12000 se jyada hai aur students array ki size 10 ho.

```sql
db.batches.find({$and : [{student : {$regex : /khan/}}, {batchName : "Design"}, {totalFee : {$gt : 12000}}, {student : {$size : 10}}]});
```
# MongoDB : let's dive deep into it...

(apollopractice naame ekta database rakha ache mongo te, jar moddhe test naame ekta collection ache)

1. use db -> change database.
2. show collections -> will show collections in current db
3. db.users.find() -> will show all the documents in the collection
4. db.users.find().count() -> how much data are there in the collection
5. db.users.find({age: 23}) -> 23 bochor boyoshi joto user ache tader dekhabe
6. db.users.find().projection({\_id: 0}) -> shob data dekhabe, kintu \_id property chara. projection e evabe je property deya hobe, seti e mongodb ar pathabe na.

7. db.users.find({age: 23}).projection({\_id: 0}) -> 23 bochorer sob user ashbe, kintu \_id props chara
8. db.users.find({skills: 'JavaScript'}) -> skills ekta array. sekhan theke evabe data ana hocche. jodi full array match korate hpy, tahole ["JavaScript", "Python"] evabe exact array deya lagto. abar nested object thekeo data ana jay. acc er backend er 5 number module e ache.

9. db.users.find({age: {$gt: 23}}) -> 23 bochorer boro shob user ke dekhabe

10. db.users.find().sort({age: -1}) -> age gula upor theke sort hoye dekhabe
11. db.users.find().sort({age: {$ne: 23}}) -> age 23 noy, emon shob user dibe
12. db.users.find({name: {$in: ['awal', 'babul']}}) -> awal ba babul, kono document er name er value er jekono ekta holei seta ba segula return korbe
13. db.users.find({name: {$nin: ['awal', 'babul']}}) -> awal ba babul, kono document er name er value eigula baade jegular, segula return korbe

14. db.users.find({$and: [{name: 'David'}, {age: 25}]}) -> logical and operator, ekhane sudhumatro jader naam David ebong ekoi sathe age 25, sudhu tader e return korbe. but kahini ta hocche, ekhane and operator use na kore direct db.users.find({name: 'David', age: 25}) dileo same kahini tai hoto.

15. db.users.find({$and: [{name: 'David'}, {age: 25}]}) -> And operator er cheye ekhetre beshi karjokori or operator. jekono keta sotto holei return korbe.
16. db.users.find({age: {$not: {$gt: 25} }}) -> not operator. ekhane sorboccho 25 bochor boyoshi user der return korbe sudhu.
17. db.users.find({$and: [{name: 'Emily'}, {age: {$gt: 25, $lt: 30}}]}) -> logical ar comparison operator combined kore use kora hyeche.
18. db.users.find({$and: [{age: {$exists: true}}) -> jeshob document e sudhu age ache, segulai return korbe
19. db.users.find({name: {$regex: /da/i}}) -> evabe regex use korte hoy. {name: { $regex: /^.{4}$/ } } eta dile jeshob doc e name property exact 5 character e,exactly oi doc gulai return korbe

20.db.expense.find({$expr: {$gt: ["$budget", "$spent"]}}) -> eta hocche expression operator. ekhane jeshob doc e budget spent er cheye boro, segula return korbe

21. db.users.updateOne({\_id: Ob......}, {$set: {name: "......."}}) -> update a document
22. db.users.updateMany({age: {$lt: 18}}, {$set: {age: 18}}) -> 18 bochorer nicher shobar age 18 baniye dibe
23. db.users.updateMany({age: {$lt: 18}}, {$inc: {age: 2}}) -> 18 bochorer nicher shobar age er sathe 2 kore jog kore dibe
24. db.collectionname.insertOne({name: "....", age: 23, skills: ["JavaScript", "Python"]}) -> insert a document
25. db.collectionname.insertMany([{name: "....", age: 23, skills: ["JavaScript", "Python"]}, {name: "....", age: 23, skills: ["JavaScript", "Python"]}]) -> insert many documents
26. db.collectionname.findOne({name: "...."}) -> first document with the name
27. db.collectionname.find({gender: "Male"}).project({name: 1, email: 1}) -> only male peoples name and email will be sent
28. db.collectionname.findOne({gender: 'Male}, {name: 1}) ->the first male person's name will be sent, this is called field projection or filtering
29. db.collectionname.find({age: {$gt: 18}}).sort({age: -1}) -> all the people whose age is greater than 18 will be sent, and they will be sorted in descending order

30. db.collectionname.find({$and: [{age: {$gt: 18}}, {age: {$lt: 30}}]}) -> all the people whose age is greater than 18 and less than 30 will be sent
31. db.collectionname.find({$or: [{interests: 'travelling'}, {interests: 'cooking'}]}) -> all the people who is interested in travelling or cooking, will be sent

32. db.collectionname.find({age: {$exists: true}}) -> all the people who has age property, will be sent
33. db.collectionname.find({age: {$type: 'number'}}) -> all the people who has age property, and the type of age property is number, will be sent
34. db.collectionname.find({age: {$mod: [5, 0]}}) -> all the people who has age property, and the age is divisible by 5, will be sent
35. db.collectionname.find({friends: {$size: 2}}) -> all the people who has friends property, and the length of friends array is 2, will be sent
36. db.collectionname.find({interests: {$all: ['travelling', 'cooking']}}) -> all the people who has interests property, and the interests array has travelling and cooking both, will be sent. if we dont use $all, mongodb will send those people who has interest in travelling , cooking in a serial order. but if we use $all, then mongodb will send those people who has interest in travelling and cooking both, no matter in which order they are in the interests array

37. db.collectionname.find({person: {$elemMatch: {name: 'John', age: 23}}}) -> kono array of object ba array theke more flexibilly data ana jay. ekhane person array er moddhe jodi name John ebong age 23 thake, tahole oi array ta return korbe

38. db.collectionname.updateOne({_id: ObjectId: '....'}, {$set: {name: '....'}}) -> updates a documents any non array property
39. db.collectionname.updateOne({_id: ObjectId: '....'}, {$addToSet: friends: 'abul'}) -> updates a documents friends property. difference between set and addToSet is that, set can add duplicate value, but addToSet can not add duplicate value. also, addToSet can add multiple values at a time. also, addToSet can add a value to an array property keeping all the previous ones untouched, but set can add value only to a non array property.

40. db.test.updateOne(
  { _id: ObjectId('6406ad63fc13ae5a40000065') },
  {
    $addToSet: {
      languages: { $each: ['hindi', 'english'] }
    }
  }
);
 -> this is how addtoset can add multiple values at a time using $each

41. 
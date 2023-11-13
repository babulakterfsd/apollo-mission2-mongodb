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

41. db.test.updateOne(
  { _id: ObjectId('6406ad63fc13ae5a40000065') },
  {
    $push: {
      languages: { $each: ['hindi', 'english'] }
    }
  }
); -> $push doesnt care if the value is duplicate or not. it will add the value to the array property. also, it can add multiple values at a time using $each or single value like : $push: {languages: 'hindi'}

42. db.collectionname.updateOne({_id: ObjectId: '....'}, {$unset: {name: ''}}) -> jodi unset use kore name property ta remove kora jay
43. db.collectionname.updateOne({_id: ObjectId: '....'}, {$rename: {name: 'fullname'}}) -> jodi rename use kore name property ta rename kora jay
44. db.collectionname.updateOne({_id: ObjectId: '....'}, {$inc: {age: 2}}) -> jodi inc use kore age property er value ta 2 kore barano jay
45. db.collectionname.updateOne({_id: ObjectId: '....'}, {$mul: {age: 2}}) -> jodi mul use kore age property er value ta 2 kore gun kora jay
46. db.collectionname.updateOne({_id: ObjectId: '....'}, {$pop: languages: 1 }) -> languages array er last element ta remove hoye jabe. ar -1 dile first element ta remove hoye jabe

## aggregation 

-> first stage e match, second stage e project, third stage e group, fourth stage e sort, fifth stage e limit, sixth stage e skip kore data ante hoy aggregation er maddhome. tobe eta oicchik. jekono stage dorkar na hole use na korleo cholbe. tobe mathay rakhte hobe je, first stage je data gulo par korbe, shei data gulo second stage e jabe, second stage je data gulo par korbe, shei data gulo third stage e jabe, and so on. tai ultapalta korle data gulo pawa jabe na.

1. db.test.aggregate([
  //stage 1 - match
  {$match: {email: 'babulakterfsd@gmail.com', age: {$lt: 25}}},
  //stage 2 - project
  {$project: {_id: 0, email: 1, age: 1, gender: 1}},

]) -> ekhane prothome email diye match kore age 25 er nicher data gula neya hoyeche, tarpor oi datagulor just email, age ar gender pathano hoyeche.

2. db.test.aggregate([
  {$match: {email: 'babulakterfsd@gmail.com', age: {$lt: 25}}},
  {$addFields: {course: 'Next level web development'}},
  {$project: {_id: 0, email: 1, age: 1, gender: 1, course: 1}}
]) -> addFields er maddhome notun field add kora hoy, kintu eta shorashori existing document e ashole add hoy na. kintu amar jodi notun ekta collection dorkar hoy jekhane existing property er sathe addFields er property gula soho notun document diye collection toiri hobe, tokhn nicher moto kore $out use kore kora jabe :

  db.test.aggregate([
  {$match: {email: 'babulakterfsd@gmail.com', age: {$lt: 25}}},
  {$addFields: {course: 'Next level web development'}},
  {$project: {_id: 0, email: 1, age: 1, gender: 1, course: 1}},
  {$out: 'newCollection'}
]) -> kintu oi je kheyal rakhte hobe, ami notun collection toiri korar aage project korchi, tai notun collection e sudhu oi property gulo niyei document gulo thakbe

3. kintu jodi chai existing collection ei document gulate notun field add korbo, tahole $merge use korte hobe evabe:
    db.test.aggregate([
  {$match: {gender: 'Male'}},
  {$addFields: {course: 'Next level web development'}},
  {$merge: 'test'}
]) -> $merge er value je collection dibo, sei collection e add hobe

4. group kore kono nirdishto field onujayee koto gula document ache set ber kora jay evabe :
   db.test.aggregate([
  {$group: {_id: "$gender", count: {"$sum" : 1}}}
]) -> amake dekhabe kon gender er koto jon ache ei collection e

arekta example :
  db.test.aggregate([
  {$group: {_id: "$address.country", count: {"$sum" : 1}}}
]) -> prottekta desher koyjon kore ache tader naam dekhabe. ar jodi desher loker puro details dekhte chai taile evabe korte hobe:

  db.test.aggregate([
  {$group: {_id: "$address.country", people: {$push: "$$ROOT"}}}
])

arekta example :
  db.test.aggregate([
  {$group: {_id: "$address.country", people: {$push: "$$ROOT"}}},
  {$prject: {"people.address": 1, "people.email": 1, "people.age": 1}}
]) -> ekhane project use kore dekhano hoyeche

5. jodi kono collection er prottekta document miliye kono calculation chalate hoy, tahole id null nile shob ekta document hishebe dhore nibe mongodb. tkhn calculation easy hobe. jemon test collection e thaka 99 joner totalsalary ber korte evabe korte hobe :

   db.test.aggregate([
  {$group: {_id: null, totalsalary: {$sum: "$salary"}}}
])

ar jodi max salary ber korte hoy tahole evabe korte hoy:
  db.test.aggregate([
  {$group: {_id: null, maxsalary: {$max: "$salary"}}}
])

6. dhorlam test collection theke amake ber korte hobe ekta nirdishto boyosh group er loker ki ki interest ache. ekhon interests ache amar collection e array hishebe. array er upore to ami action nite partesi na. tai array ta ke vengge individual doc e convert korte hobe first e . ar eikhnei chole ashe $unwind. ei unwind ekta array ke vengge individual doc toiri kore. example :

db.test.aggregate([
  {$unwind: "$interests"},
  {$group: {_id: {age: "$age", interests: "$interests"}, count: {$sum: 1}}}
]) -> ekhane unwind er maddhome interests array ta vengge individual doc toiri hoyeche. ar tarpor group er maddhome amra ber korte chai je, kon age er loker ki ki interest ache. tai age ar interest er upore group kore count ber kora hoyeche

7. db.test.aggregate([
  {$unwind: "$interests"},
  {$group: {_id: "$age", interestsPerAge: {$push: "$interests"}}}
]) -> ekhane unwind er maddhome interests array ta vengge individual doc toiri hoyeche. ar tarpor group er maddhome amra ber korte chai je, kon age er loker ki ki interest ache. tai age ar interest er upore group kore count ber kora hoyeche

8. $bucket use korar maddhome boundary kore kore group kora jay evabe:

   db.test.aggregate([
  {$bucket: {groupBy: "$age", boundaries: [20, 40, 60], default: '60 bochorer uporer manushjon', output: {count: {$sum: 1}}}}
  ]) -> ekhane 0 theke 20, 21 theke 40, 41 theke 60, 60 er upore er manushjon er count ber kora hoyeche. chaile push use kore tader full data o pathano jabe evabe:
    
    db.test.aggregate([
  {$bucket: {groupBy: "$age", boundaries: [20, 40, 60], default: '60 bochorer uporer manushjon', output: {count: {$sum: 1, people: {$push: "$$ROOT"}}}}}
  ])

  abar ekhane amra count er upor vitti kore sort kore dekhbo:

  db.test.aggregate([
  {$bucket: {groupBy: "$age", boundaries: [20, 40, 60], default: '60 bochorer uporer manushjon', output: {count: {$sum: 1, people: {$push: "$$ROOT"}}}}},
  {$sort: {count: -1}
  ])

shob cheye boro group of people ber korlam evabe:
  db.test.aggregate([
  {$bucket: {groupBy: "$age", boundaries: [20, 40, 60], default: '60 bochorer uporer manushjon', output: {count: {$sum: 1}}}},
  {$sort: {count: -1}},
  {$limit: 1}
  ])



9. faceet er maddhome multi pipeline use kora hoy evabe :

   db.test.aggregate([
  {$facet: {facet1: [{$match: {age: {$lt: 25}}}, {$project: {_id: 0, name: 1, age: 1}}], facet2: [{$match: {age: {$gte: 25}}}, {$project: {_id: 0, name: 1, age: 1}}]}}
  ])

10. db.orders.aggregate([
  {
  $lookup: {
    from: "test", -> kon collection theke data ante chai
    localField: "userId", -> ami je collection e achi, shei collection er kon field diye data ante chai
    foreignField: "_id", -> ami je collection theke data ante chai, shei collection er kon field er sathe match korte chai
    as: "Who has Ordered" -> je data ta anbo, seti ki naame show korbe
}}
]) -> evabe $lookup use kore ek collection er datar sathe referencing kore onno collection er data niye asha jay. eta khub e powerful ebong dorkari.


11. details dekhar jonno evabe command likhte hoy : db.test.find({email: 'hello@gmail.com'}).explain("executionStats")
12. boro datar collection gulate taratari query korar jonno indexing kora hoy evabe :

    db.orders.createIndex({email: 1}) -> 1 mane ascending order, -1 mane descending order. ami email diye index korlam. ekhon jodi email diye data khuji, taile _id er motoi druto paoa jabe.

13. db.orders.createIndex({email: 1}, {unique: true}) -> ekhane unique true kore dilam. tai jodi ekta email diye 2 ta order kora hoy, tahole error dekhabe. karon email unique hote hobe.

14. indexing remove korte dropIndex use kora hoy. example :

    db.orders.dropIndex({email: 1})

15. search index kora hoy evabe :

    db.orders.createIndex({email: 'text'})

    tarpor search korar jonno :
     
      db.orders.find({$text: {$search: "gmail"}})

      tahole gmail er sathe match kore jei email ache, shei email gulo show korbe


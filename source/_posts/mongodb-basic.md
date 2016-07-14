title: MongoDB基本语句
date: 2016-02-19 21:01:36
categories: 归纳整理 #文章文类
tags: [MongoDB] #文章标签，多于一项时用这种格式
---
MongoDB无模式文档型数据库

1.批量插入insert
```
    db.person.insert([
     {name:"Mary",  age:21, status:"A"},
     {name:"Lucy",  age:89, status:"A"},
     {name:"Jacky", age:30, status:"A"} 
    ]);
```
2.文档查询find
```
    db.person.find();
    db.user.find(
        {age:{$gt:18}},
        {name:1,address:1}
    ).limit(5);
    db.person.find({status:"X"});//相等条件
    db.person.find({age:{$gt:40}});//比较条件
```
    MongoDB运算符：大于$gt,小于$lt,大于等于$gte,小于等于$lte,不等于$ne,包含于$in,不包含于$nin
```
    db.person.find({tag:'fruit'});//单个元素匹配
    db.person.find({tag.0:'fruit'});//多个元素匹配
    db.person.find({"access.level":5});//子文档条件，使用“.key”的方法去访问
    //复合查询：
    db.person.find({$and:[{type:"food"},{price:{$lt:95}}]});
    db.person.find({$and:[{age:{$gt:30}},{name:"Lucy"}]});
    db.person.find({$or:[{status:"A"},{age:30}]});
```
3.文档更新update
```
    db.collection.update(query,update,{upsert:boolean,multi:boolean})
    db.person.update({age:{$lt:30}},{$set:{status:"X"}},{multi:true})//$gt为大于，$lt为小于
```
4.文档更新save 
    命令可以更新或插入一个新文档，只能针对一个文档进行操作
    db.person.save({name:"Tony",age:12,gender:"man"});
5.文档移除remove 
```
    db.collection.remove(
        qurey, //boolean类型，删除文档的条件
        justOne //为true只删除一个文档，为false则删除所有符合条件的文档    
    )
    db.person.remove(
        {status:"D"}
    )
```
6.游标 cursor
    find命令并不直接返回结果，而是返回一个结果集的迭代器
    想要获得结果，必须使用next方法来遍历游标
```
    var myCursor = db.person.find({status:"A"});
    var myDocument = myCursor.hasNext()?myCursor.next():null;
    if(myDocument){
        var myItem =myDocument.item;
        print(tojson(myItme));
    }
    
    var myCursor = db.person.find({status:"A"});
    myCursor.forEach(printjson);
```
    a)限定条件
    limit:设定返回结果集中的最大文档数量；
    db.collection.find().limit(Num);
    b)结果集
    条件：JSON对象，格式=>{字段：值}，值为1时表示需要返回，值为0时表示不需要返回
    db.person.find({查询条件},{字段条件})
    db.person.find({},{name:1});


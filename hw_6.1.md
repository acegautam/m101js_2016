```javascript

db.companies.aggregate([
    { $match:{"relationships.person": { $ne: null } } },
    { $unwind: "$relationships" },
    { $group: {
        "_id": "$relationships.person",        
        unique_relation: { $addToSet: "$permalink" }        
      } 
    },
    { $match:{"_id.permalink": {$in: ["eric-di-benedetto", "roger-ehrenberg", "josh-stein", "tim-hanlon"]}  } },
    { $project: {
        "name": "$_id.permalink",
        "count": { $size: "$unique_relation"}
     } },
    { $sort: {"_id.permalink": 1} }
]);

```

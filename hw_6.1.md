```javascript

db.companies.aggregate([
    { $match:{"relationships.person": { $ne: null } } },
    { $unwind: "$relationships" },
    { $group: {
        "_id": "$relationships.person",        
        unique_relation: { $addToSet: "$permalink" }        
      } 
    },
    { $project: {
        "name": "$_id.permalink",
        "count": { $size: "$unique_relation"}
     } },
    { $sort: {count: -1} }
]);

```

```javascript
db.getCollection('companies').aggregate([
    { $match: {"founded_year":2004, "funding_rounds": { $exists: true, $ne: [] } } },
    { $project: {
        _id: 0,
        name: 1,
        funding_rounds: 1,
        rounds: { $size: "$funding_rounds"},
        avg_fund_amount: {$avg: "$funding_rounds.raised_amount"}
    } },
    { $match: {"rounds": {$gte: 5} }},
    { $sort: {"avg_fund_amount": 1} }
])
```

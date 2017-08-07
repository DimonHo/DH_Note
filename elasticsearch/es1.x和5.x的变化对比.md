## 过滤
1.x:
```
{
  "filter": [
      { "range": { "born": { "gte": "1874" }}}
  ]
}
```
5.x:
```
{
    "query": { 
        "bool": {
            "filter": [
                { "range": { "born": { "gte": "1874" }}}
            ]
        }
    }
}
```

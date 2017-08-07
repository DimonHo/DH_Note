### 过滤
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

### exists 和 missing
5.x已经不支持missing过滤，只保留了exists。如果需要查询missing，请用not exists.

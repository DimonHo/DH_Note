### 配置文件参数变化
|before 5.x|after 5.x|
|:--------|:---------|
|discovery.zen.ping.timeout: 3s | discovery.zen.ping_timeout: 3s|
|bootstrap.mlockall: true | bootstrap.memory_lock: true|



### scroll API
- 1.x:(https://www.elastic.co/guide/en/elasticsearch/reference/1.3/search-request-scroll.html)
```
curl -XGET 'localhost:9200/twitter/tweet/_search?scroll=1m' -d '
{
    "query": {
        "match" : {
            "title" : "elasticsearch"
        }
    }
}

curl -XGET  'localhost:9200/_search/scroll?scroll=1m' -d  'c2Nhbjs2OzM0NDg1ODpzRlBLc0FXNlNyNm5JWUc1' 
or
curl -XGET  'localhost:9200/_search/scroll?scroll=1m&scroll_id=c2Nhbjs2OzM0NDg1ODpzRlBLc0FXNlNyNm5JWUc1'
```
- 5.x:取消了search_type=scan(https://www.elastic.co/guide/en/elasticsearch/reference/5.5/search-request-scroll.html)
```
POST /twitter/tweet/_search?scroll=1m
{
    "size": 100,
    "query": {
        "match" : {
            "title" : "elasticsearch"
        }
    }
}

POST  /_search/scroll 
{
    "scroll" : "1m", 
    "scroll_id" : "DXF1ZXJ5QW5kRmV0Y2gBAAAAAAAAAD4WYm9laVYtZndUQlNsdDcwakFMNjU1QQ==" 
}
```
### 过滤
- 1.x:
```
{
  "filter": [
      { "range": { "born": { "gte": "1874" }}}
  ]
}
```
- 5.x:
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
5.x已经不支持missing过滤，只保留了exists。如果需要查询missing，请用must_not exists.
- 1.x:
```
{
  "filter": {
    "missing": {
      "field": "issn"
    }
  }
}
```
- 5.x:
```
{
  "query": {
    "bool": {
      "filter": {
        "bool": {
          "must_not": [
            {
              "exists": {
                "field": "issn"
              }
            }
          ]
        }
      }
    }
  }
}
```

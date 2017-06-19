
### es返回特定字段的JAVA API示例
```java
/**
 * @param client  es客户端
 * @param index   index的名称
 * @param type    type的名称
 * @param queryBuilder    查询条件
 * @param fields    返回字段列表
 * @return
 */
public SearchHits getFieldData(Client client,String index,String type,QueryBuilder queryBuilder, String[] fields) {
  SearchRequest request = new SearchRequest();
  request.indices(index).types(type);
  SearchSourceBuilder searchSourceBuilder = new SearchSourceBuilder();
  if(fields != null){
    FetchSourceContext sourceContext = new FetchSourceContext(fields);
    searchSourceBuilder.fetchSource(sourceContext);
  }
  searchSourceBuilder.query(queryBuilder);
  request.extraSource(searchSourceBuilder);

  return client.search(request).actionGet().getHits();
}
```

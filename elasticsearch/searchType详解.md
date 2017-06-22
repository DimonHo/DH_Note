`GET myindex/mytype/_search?search_type=query_then_fetch` 

- query_then_fetch ##默认的搜索模式，向每个分片查询，并统计得分情况，返回给客户端的结果数量等于指定的size大小，排序相对精确，但每次返回的结果排序可能不一致。  
- query_and_fetch   ##每个分片都返回size个结果一起返回给客户端，返回结果数量等于(size X 分片数)。  
- dfs_query_then_fetch  ##向所有的分片查询，返回给客户端的结果数量等于指定的size大小，排序更为精确，每次请求排序是一致的。  
- dfs_query_and_fetch   ##每个分片都返回size个结果一起返回给客户端，返回结果数量等于(size X 分片数)。  
- scan  ##向每个分片请求size个结果，返回结果数量等于(size X 分片数)。不计算相关性分数，不排序。仅用于scroll查询。
- count ##只返回匹配数目，不返回实际数据。

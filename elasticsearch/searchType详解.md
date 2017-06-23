`GET myindex/mytype/_search?search_type=query_then_fetch` 

## 四种基础搜索类型
- **query_then_fetch:**   ##如果你搜索时，没有指定搜索方式，就是使用的这种搜索方式。这种搜索方式，大概分两个步骤，第一步，先向所有的分片（shard）发出请求，各分片只返回排序和排名相关的信息（注意:不包括文档document)，然后按照各分片返回的分数进行重新排序和排名，取前size个文档。然后进行第二步，去相关的shard取document。这种方式返回的document与用户要求的size是相等的。
- **query_and_fetch:**    ##向索引的所有分片（shard）都发出查询请求，各分片返回的时候把元素文档（document）和计算后的排名信息一起返回。这种搜索方式是最快的。因为相比其它几种搜索方式，这种查询方法只需要去shard查询一次。但是各个shard返回的结果的数量之和是用户要求的size乘以分片数的数量。
- **dfs_query_then_fetch:**    ##向所有的分片查询，返回给客户端的结果数量等于指定的size大小，排序更为精确，每次请求排序是一致的。  
- **dfs_query_and_fetch:**   ##每个分片都返回size个结果一起返回给客户端，返回结果数量等于(size X 分片数)。  

*效率方面：query_and_fetch最快，dfs_query_then_fetch最慢*   
*排序精度：dfs_query_then_fetch最好，query_and_fetch最差*   


## 两种特殊搜索类型
- **scan:**    ##向每个分片请求size个结果，返回结果数量等于(size X 分片数)。不计算相关性分数，不排序。仅用于scroll查询。
- **count:**   ##只返回匹配数目，不返回实际document。



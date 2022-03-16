# Bool

### Example

get document using `and` operator

```json
GET /bank/_search
{
  "query": {
    "bool": {
      "must": [
        { "match": { "age": "40" } }
      ],
      "must_not": [
        { "match": { "state": "ID" } }
      ]
    }
  }
}
```



### References

* [https://www.elastic.co/guide/kr/elasticsearch/reference/current/gs-executing-searches.html](https://www.elastic.co/guide/kr/elasticsearch/reference/current/gs-executing-searches.html)
* [https://www.elastic.co/guide/en/elasticsearch/reference/5.4/query-dsl-bool-query.html](https://www.elastic.co/guide/en/elasticsearch/reference/5.4/query-dsl-bool-query.html)

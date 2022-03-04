# Query

{% hint style="info" %}
Below queries use data from [kaggle](https://www.kaggle.com/rmisra/news-category-dataset)
{% endhint %}

### Grep documents

#### query all

return all of index's documents. default return 10 documents.

also response has total document count. but not perfect.

```http
GET news_headlines/_search
```

```json
...
"hits": {
    "total": 10000,
    "relation": "gte"
    },
...
```

#### track\_total\_hits

order query to tracking all hit documents.

```json
GET news_headlines/_search
{
    "track_total_hits": true
}
```

```json
...
"hits": {
    "total": {
        "value": 200853,
        "relation": "eq"
    },
...
```

now we can see property `relation`'s value gonna `eq` as equal.



### Make boundaries

#### Range

return documents write down 2015 and between "06-20" and "09-22"

```json
GET news_headlines/_search
{
    "query": {
        "range": {
            "date": {
                "gte": "2015-06-20",
                "lte": "2015-09-22"
            }
        }
    }
}
```

### Aggregations

return documents about "category"

```json5
GET news_headlines/_search
{
  "aggs": {
    "by_category": {
      "terms": {
        "field": "category",
        "size": 100
      }
    }
  }
}
```

This time we do not check property "hits". check "aggregations"

response like below:

```json
"hits": { ... },
"aggregations": {
    "by_category": {
        "doc_count_error_upper_bound": 0,
        "sum_other_doc_count": 80845,
        "buckets": [
        {
            "key": "POLITICS",
            "doc_count": 32739
        },
        {
            "key": "WELLNESS",
            "doc_count": 17827
        },
...
```

and next, let's combine query and aggregation.

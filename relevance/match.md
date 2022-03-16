---
description: this page describe about match command
---

# Match

### Combination

search for <mark style="color:red;">the most significant term</mark> in a category.

```json
GET news_headlines/_search
{
  "query": {
    "match": {
      "category": "ENTERTAINMENT"
    }
  },
  "aggregations": {
    "popular_in_entertainment": {
      "significant_text": {
        "field": "headline"
      }
    }
  }
}
```

result is:

```json
"hits": { ... },
"aggregations": {
    "my_sample": {
        "doc_count": 16058,
        "bg_count": 200853,
        "buckets": [
        {
            "key": "trailers",
            "doc_count": 387,
            "score": 0.21944632913239076,
            "bg_count": 479
        },
        {            
            "key": "movie",
            "doc_count": 419,
            "score": 0.16123418320234606,
            "bg_count": 730
        },
...
```

### Precision and Recall

#### Simple match

match query use "OR" logic as default. it means:

```python
# below pseudo-code not describe about string OR operation.
query = "Kloe" | "Kardashian" | "Kendall" | "Jenner"
```

```json
GET news_headlines/_search
{
  "query": {
    "match": {
      "headline": {
        "query": "Khloe Kardashian Kendall Jenner"
      }
    }
  }
}
```

![https://github.com/LisaHJung/Part-2-Understanding-the-relevance-of-your-search-with-Elasticsearch-and-Kibana-#precision-and-recall](<../.gitbook/assets/image (2).png>)

found too many documents. need to increase precision.

#### Increase precision

update query using `AND` operator

```json
GET news_headlines/_search
{
  "query": {
    "match": {
      "headline": {
        "query": "Khloe Kardashian Kendall Jenner",
        "operator": "and"
      }
    }
  }
}
```

```json
...
"hits": {
    "total": {
        "value": 1,
        "relation": "eq"
    },
...
```

as you see, we got only 1 document. precision increased but not what expected.

#### minimum\_should\_match

```json
GET news_headlines/_search
{
  "query": {
    "match": {
      "headline": {
        "query": "Khloe Kardashian Kendall Jenner",
        "minimum_should_match": 3
      }
    }
  }
}
```

```json
...
"hits": {
    "total": {
        "value": 6,
        "relation": "eq"
    },
...
```

we got 5 more documents.

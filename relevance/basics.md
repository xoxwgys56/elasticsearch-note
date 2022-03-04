# Basics

`elastic search에서 무엇을 검색한 경우, 유사한 것들에 대해 검색 결과를 반환합니다.`

### Precision

![image from https://youtu.be/CCTgroOcyfM?t=494](<../.gitbook/assets/image (2) (1) (1).png>)

What portion of the retrieved data is actually relevant to the search query?

### Recall

![image from https://youtu.be/CCTgroOcyfM?t=518](<../.gitbook/assets/image (4).png>)

What portion of relevant data is being returned as search results?

**Precision** and **Recall** are inversely related. like:

- **Precision**
  - query와 완벽히 매치되는 결과를 반환.
  - 반환되는 document가 적을 수 있음.
- Recall
  - retrieve lot of result
  - 많은 결과를 반환.
  - query에 대해 완벽히 매치되는 document가 아닐 수 있음.

### Score

- value that represents how relevant a document is to that specific query
- score is computed for each document that is a hit.
- score use 2 type of data.
  - term frequency
  - inverse document frequency

#### TF (Term Frequency)

for example, let's say search term is "How to form good habits"

![https://youtu.be/CCTgroOcyfM?t=830](<../.gitbook/assets/image (5).png>)

#### IDF (Inverse Document Frequency)

IDF decrease weight which occur very frequently. our case, _habit_ occurred very frequently.

![https://youtu.be/CCTgroOcyfM?t=830](<../.gitbook/assets/image (6).png>)

#### `References`

- [https://esbook.kimjmin.net/05-search/5.3-relevancy](https://esbook.kimjmin.net/05-search/5.3-relevancy)

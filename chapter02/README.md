# 2장. 시작해보기

- https://github.com/madhusudhankonda/elasticsearch-in-action/wiki/Ch-2:-Getting-Started

## Indexing

### Indexing the book document using Kibana tool

```shell
PUT books/_doc/1
{
    "title": "Effective Java",
    "author": "Joshua Bloch",
    "release_date": "2001-06-01",
    "amazon_rating": 4.7,
    "best_seller": true,
    "prices": {
        "usd": 9.95,
        "gbp": 7.95,
        "eur": 8.95
    }
}
```

### Index More Documents

```shell
PUT books/_doc/2
{
    "title": "Core Java Volume I - Fundamentals",
    "author": "Cay S. Horstmann",
    "release_date": "2018-08-27",
    "amazon_rating": 4.8,
    "best_seller": true,
    "prices": {
        "usd": 19.95,
        "gbp": 17.95,
        "eur": 18.95
    }
}

PUT books/_doc/3
{
    "title": "Java: A Beginner's Guide",
    "author": "Herbert Schildt",
    "release_date": "2018-11-20",
    "amazon_rating": 4.2,
    "best_seller": true,
    "prices": {
        "usd": 19.99,
        "gbp": 19.99,
        "eur": 19.99
    }
}
```

## Counting

### Counting all documents

```shell
GET books/_count
```

### Fetching the document by ID

```shell
GET books/_doc/1
```

### Fetching multiple documents

```shell
GET books/_search
{
    "query": {
        "ids": {
            "values": [1,2,3]
        }
    }
}
```

## Searching

### Retrieving all documents

```shell
GET books/_search
```

### Search a Book Written By a Specific Author

```shell
GET books/_search
{
    "query": {
        "match": {
            "author": "Joshua"
        }
    }
}
```

### Search with an Exact Title

```shell
GET books/_search
{
    "query": {
        "match": {
            "title": {
                "query": "Effective java",
                "operator": "and"
            }
        }
    }
}
```

## Bulk

### Indexing Multiple Documents using _bulk API

- https://github.com/madhusudhankonda/elasticsearch-in-action/blob/main/datasets/books-kibana-dataset.txt

```shell
POST _bulk
{"index":{"_index":"books","_id":"1"}}
{"title": "Core Java Volume I – Fundamentals","author": "Cay S. Horstmann","edition": 11, "synopsis": "Java reference book that offers a detailed explanation of various features of Core Java, including exception handling, interfaces, and lambda expressions. Significant highlights of the book include simple language, conciseness, and detailed examples.","amazon_rating": 4.6,"release_date": "2018-08-27","tags": ["Programming Languages, Java Programming"]}
{"index":{"_index":"books","_id":"2"}}
{"title": "Effective Java","author": "Joshua Bloch", "edition": 3,"synopsis": "A must-have book for every Java programmer and Java aspirant, Effective Java makes up for an excellent complementary read with other Java books or learning material. The book offers 78 best practices to follow for making the code better.", "amazon_rating": 4.7, "release_date": "2017-12-27", "tags": ["Object Oriented Software Design"]}
{"index":{"_index":"books","_id":"3"}}
{"title": "Java: A Beginner’s Guide", "author": "Herbert Schildt","edition": 8,"synopsis": "One of the most comprehensive books for learning Java. The book offers several hands-on exercises as well as a quiz section at the end of every chapter to let the readers self-evaluate their learning.","amazon_rating": 4.2,"release_date": "2018-11-20","tags": ["Software Design & Engineering", "Internet & Web"]}
{"index":{"_index":"books","_id":"4"}}
{"title": "Java - The Complete Reference","author": "Herbert Schildt","edition": 11,"synopsis": "Convenient Java reference book examining essential portions of the Java API library, Java. The book is full of discussions and apt examples to better Java learning.","amazon_rating": 4.4,"release_date": "2019-03-19","tags": ["Software Design & Engineering", "Internet & Web", "Computer Programming Language & Tool"]}
{"index":{"_index":"books","_id":"5"}}
{"title": "Head First Java","author": "Kathy Sierra and Bert Bates","edition":2, "synopsis": "The most important selling points of Head First Java is its simplicity and super-effective real-life analogies that pertain to the Java programming concepts.","amazon_rating": 4.3,"release_date": "2005-02-18","tags": ["IT Certification Exams", "Object-Oriented Software Design","Design Pattern Programming"]}
{"index":{"_index":"books","_id":"6"}}
{"title": "Java Concurrency in Practice","author": "Brian Goetz with Tim Peierls, Joshua Bloch, Joseph Bowbeer, David Holmes, and Doug Lea","edition": 1,"synopsis": "Java Concurrency in Practice is one of the best Java programming books to develop a rich understanding of concurrency and multithreading.","amazon_rating": 4.3,"release_date": "2006-05-09","tags": ["Computer Science Books", "Programming Languages", "Java Programming"]}
{"index":{"_index":"books","_id":"7"}}
{"title": "Test-Driven: TDD and Acceptance TDD for Java Developers","author": "Lasse Koskela","edition": 1,"synopsis": "Test-Driven is an excellent book for learning how to write unique automation testing programs. It is a must-have book for those Java developers that prioritize code quality as well as have a knack for writing unit, integration, and automation tests.","amazon_rating": 4.1,"release_date": "2007-10-22","tags": ["Software Architecture", "Software Design & Engineering", "Java Programming"]}
{"index":{"_index":"books","_id":"8"}}
{"title": "Head First Object-Oriented Analysis Design","author": "Brett D. McLaughlin, Gary Pollice & David West","edition": 1,"synopsis": "Head First is one of the most beautiful finest book series ever written on Java programming language. Another gem in the series is the Head First Object-Oriented Analysis Design.","amazon_rating": 3.9,"release_date": "2014-04-29","tags": ["Introductory & Beginning Programming", "Object-Oriented Software Design", "Java Programming"]}
{"index":{"_index":"books","_id":"9"}}
{"title": "Java Performance: The Definite Guide","author": "Scott Oaks","edition": 1,"synopsis": "Garbage collection, JVM, and performance tuning are some of the most favorable aspects of the Java programming language. It educates readers about maximizing Java threading and synchronization performance features, improve Java-driven database application performance, tackle performance issues","amazon_rating": 4.1,"release_date": "2014-03-04","tags": ["Design Pattern Programming", "Object-Oriented Software Design", "Computer Programming Language & Tool"]}
{"index":{"_index":"books","_id":"10"}}
{"title": "Head First Design Patterns", "author": "Eric Freeman & Elisabeth Robson with Kathy Sierra & Bert Bates","edition": 10,"synopsis": "Head First Design Patterns is one of the leading books to build that particular understanding of the Java programming language." ,"amazon_rating": 4.5,"release_date": "2014-03-04","tags": ["Design Pattern Programming", "Object-Oriented Software Design eTextbooks", "Web Development & Design eTextbooks"]}
```

## Search Query

### Matching a Word Across Multiple Fields

```shell
GET books/_search
{
    "_source": {
        "includes": "title"
    },
    "query": {
        "multi_match": {
        "query": "Java",
            "fields": ["title","synopsis"]
        }
    }
}
```

### Boosting Queries

```shell
GET books/_search
{
    "_source": {
        "includes": ["title","synopsis"]
    },
    "query": {
        "multi_match": {
        "query": "Java",
            "fields": ["title^3","synopsis"]
        }
    }
}
```

### Searching for a phrase

```shell
GET books/_search
{
    "query": {
        "match_phrase": {
            "synopsis": "must-have book for every Java programmer"
        }
    }
}
```

### Match phrase query with highlights

```shell
GET books/_search
{
    "query": {
        "match_phrase": {
            "synopsis": "must-have book for every Java programmer"
        }
    },
    "highlight": {
        "fields": {
            "synopsis": {}
        }
    }
}
```

### Phrases with missing words

```shell
GET books/_search
{
    "query": {
        "match_phrase": {
            "synopsis": {
                "query": "must-have book every Java programmer",
                "slop": 1
            }
        }
    }
}
```

### Index adhoc documents (Not found in the book)

```shell
PUT books/_doc/99
{
    "title":"Java Collections Deep Dive"
}
PUT books/_doc/100
{
    "title":"Java Computing World"
}
```

### Matching phrases with a prefix (Not found in the book)

```shell
GET books/_search
{
    "query": {
        "match_phrase_prefix": {
            "title": "Java co"
        }
    }
}
```

### Fuzzy query

```shell
GET books/_search
{
    "query": {
        "fuzzy": {
            "title": {
                "value": "kava",
                "fuzziness": 1 
            }
        }
    }
}
```

## Term level queries

### term queries

```shell
GET books/_search
{
    "_source": ["title","edition"], 
    "query": {
        "term": { 
            "edition": { 
                "value": 3
            }
        }
    }
}
```

### Range queries

```shell
GET books/_search
{
    "query": {
        "range": {
            "amazon_rating": {
                "gte": 4.5,
                "lte": 5
            }
        }
    }
}
```

## Compound queries

### A bool query

```shell
GET books/_search
{
    "query": {
        "bool": { 
            "must": [
                {
                    "match": {
                        "author": "Joshua Bloch"
                    }
                }
            ]
        }
    }
}
```

### A must clause with multiple leaf queries

```shell
GET books/_search
{
    "query": {
        "bool": {
            "must": [
                { 
                    "match": {
                        "author": "Joshua Bloch"
                    }
                },
                {
                    "match_phrase": {
                        "synopsis": "best Java programming books"
                    }
                }
            ]
        }
    }
}
```

### The must_not clause

```shell
GET books/_search
{
    "query": {
        "bool": {
            "must": [
                {
                    "match": {
                        "author": "Joshua"
                    }
                }
            ],
            "must_not": [
                {
                    "range": {
                        "amazon_rating": {
                            "lt": 4.7
                        }
                    }
                }
            ] 
        }
    }
}
```

### The should clause

```shell
GET books/_search
{
    "query": {
        "bool": {
            "must": [
                {
                    "match": {
                        "author": "Joshua"
                    }
                }
            ],
            "must_not": [
                {
                    "range": {
                        "amazon_rating": {
                            "lt": 4.7
                        }
                    }
                }
            ],
            "should": [
                {
                    "match": {
                        "tags": "Software"
                    }
                }
            ]
        }
    }
}
```

### The filter clause

```shell
GET books/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "author": "Joshua"
          }
        }
      ],
      "must_not": [
        {
          "range": {
            "amazon_rating": {
              "lt": 4.7
            }
          }
        }
      ],
      "should": [
        {
          "match": {
            "tags": "Software"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "release_date": {
              "gte": "2015-01-01"
            }
          }
        }
      ]
    }
  }
}
```

### Filter clause with multiple leaf queries (Not found in the book)

```shell
GET books/_search
{
    "query":{
        "bool":{
            "must":[
                {
                    "match":{
                        "author":"Joshua"
                    }
                }
            ],
            "must_not":[
                {
                    "range":{
                        "amazon_rating":{
                            "lt":4.7
                        }
                    }
                }
            ],
            "should":[
                {
                    "match":{
                        "tags":"Software"
                    }
                }
            ],
            "filter":[
                {
                    "range":{
                        "release_date":{
                            "gte":"2015-01-01"
                        }
                    }
                },
                {
                    "term":{
                        "edition":3
                    }
                }
            ]
        }
    }
}
```

## Aggregations

### bulk

- https://github.com/madhusudhankonda/elasticsearch-in-action/blob/main/datasets/covid-26march2021.txt

```shell
POST covid/_bulk
{"index":{}}
{"country":"United States of America","date":"2021-03-26","cases":30853032,"deaths":561142,"recovered":23275268,"critical":8610}
{"index":{}}
{"country":"Brazil","date":"2021-03-26","cases":12407323,"deaths":307326,"recovered":10824095,"critical":8318}
{"index":{}}
{"country":"India","date":"2021-03-26","cases":11908373,"deaths":161275,"recovered":11292849,"critical":8944}
{"index":{}}
{"country":"Russia","date":"2021-03-26","cases":4501859,"deaths":97017,"recovered":4120161,"critical":2300}
{"index":{}}
{"country":"France","date":"2021-03-26","cases":4465956,"deaths":94275,"recovered":288062,"critical":4766}
{"index":{}}
{"country":"United kingdom","date":"2021-03-26","cases":4325315,"deaths":126515,"recovered":3768434,"critical":630}
{"index":{}}
{"country":"Italy","date":"2021-03-26","cases":3488619,"deaths":107256,"recovered":2814652,"critical":3628}
{"index":{}}
{"country":"Spain","date":"2021-03-26","cases":3255324,"deaths":75010,"recovered":3016247,"critical":1830}
{"index":{}}
{"country":"Turkey","date":"2021-03-26","cases":3149094,"deaths":30772,"recovered":2921037,"critical":1810}
{"index":{}}
{"country":"Germany","date":"2021-03-26","cases":2754002,"deaths":76303,"recovered":2467600,"critical":3209}
```

### Sum metric

```shell
GET covid/_search
{
    "size":0,
    "aggs":{
        "critical_patients":{
            "sum":{
                "field":"critical"
            }
        }
    }
}
```

### Max metric

```shell
GET covid/_search
{
    "size":0,
    "aggs":{
        "max_deaths":{
            "max":{
                "field":"deaths"
            }
        }
    }
}
```

### Stats metric

```shell
GET covid/_search
{
    "size":0,
    "aggs":{
        "all_stats":{
            "stats":{
                "field":"deaths"
            }
        }
    }
}
```

### Extended stats

```shell
GET covid/_search
{
    "aggs":{
        "all_extended_stats":{
            "extended_stats":{
                "field":"deaths"
            }
        }
    }
}
```

### Bucketing aggregations - Histogram buckets

```shell
GET covid/_search
{
    "size":0,
    "aggs":{
        "critical_patients_as_histogram":{
            "histogram":{
                "field":"critical",
                "interval":2500
            }
        }
    }
}
```

### Bucketing aggregations - Range buckets

```shell
GET covid/_search
{
    "size":0,
    "aggs":{
        "range_countries":{
            "range":{
                "field":"deaths",
                "ranges":[
                    {
                        "to":60000
                    },
                    {
                        "from":60000,
                        "to":70000
                    },
                    {
                        "from":70000,
                        "to":80000
                    },
                    {
                        "from":80000,
                        "to":120000
                    }
                ]
            }
        }
    }
}
```

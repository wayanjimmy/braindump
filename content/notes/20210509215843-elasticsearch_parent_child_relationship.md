+++
title = "Elasticsearch Parent Child Relationship"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Data Modeling in Elasticsearch](https://youtu.be/fPNiGjB8JR8) [Join Datatype Elasticsearch 6.8](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/parent-join.html)

related
: [Elasticsearch]({{<relref "20201221151118-elasticsearch.md#" >}}) [Handle relational data in Elasticsearch]({{<relref "20201222134415-handle_relational_data_in_elasticsearch.md#" >}})


## Must Read! {#must-read}

-   Parent and child documents must be indexed on the **same shard**. This means that the same routing value needs to be provided when getting, deleting, or updating a child document.
-   When doing reindex must provide the **routing** value, read [more](https://www.elastic.co/guide/en/elasticsearch/reference/6.8/parent-join.html#CO240-1)


## Hands on {#hands-on}


### Create Mapping {#create-mapping}

> PUT /series
> {
>   "mappings": {
>     "movie": {
>       "properties": {
>         "film\_to\_franchise": {
>           "type": "join",
>           "relations": {
>             "franchise": "film"
>           }
>         }
>       }
>     }
>   }
> }


### Import Data {#import-data}

```bash
curl -XPUT "http://localhost:9200/_bulk" -H 'Content-Type: application/json' -d'
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "1", "routing" : 1} }
{ "id": "1", "film_to_franchise": {"name": "franchise"}, "title" : "Star Wars" }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "260", "routing" : 1} }
{ "id": "260", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode IV - A New Hope", "year":"1977" , "genre":["Action", "Adventure", "Sci-Fi"] }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "1196", "routing" : 1} }
{ "id": "1196", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode V - The Empire Strikes Back", "year":"1980" , "genre":["Action", "Adventure", "Sci-Fi"] }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "1210", "routing" : 1} }
{ "id": "1210", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode VI - Return of the Jedi", "year":"1983" , "genre":["Action", "Adventure", "Sci-Fi"] }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "2628", "routing" : 1} }
{ "id": "2628", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode I - The Phantom Menace", "year":"1999" , "genre":["Action", "Adventure", "Sci-Fi"] }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "5378", "routing" : 1} }
{ "id": "5378", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode II - Attack of the Clones", "year":"2002" , "genre":["Action", "Adventure", "Sci-Fi", "IMAX"] }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "33493", "routing" : 1} }
{ "id": "33493", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode III - Revenge of the Sith", "year":"2005" , "genre":["Action", "Adventure", "Sci-Fi"] }
{ "create" : { "_index" : "series", "_type" : "movie", "_id" : "122886", "routing" : 1} }
{ "id": "122886", "film_to_franchise": {"name": "film", "parent": "1"}, "title" : "Star Wars: Episode VII - The Force Awakens", "year":"2015" , "genre":["Action", "Adventure", "Fantasy", "Sci-Fi", "IMAX"] }
'
```


### Find the Series that have parent of Star Wars {#find-the-series-that-have-parent-of-star-wars}

```bash
curl -XGET "http://es01:9200/series/movie/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "has_parent": {
      "parent_type": "franchise",
      "query": {
        "match": {
          "title": "Star Wars"
        }
      }
    }
    }
}'
```


### Find the series by it's child {#find-the-series-by-it-s-child}

```bash
GET /series/movie/_search
{
  "query": {
    "has_child": {
      "type": "film",
      "query": {
        "match": {
          "title": "The Force Awakens"
        }
      }
    }
  }
}
```

+++
title = "Reindex without downtime Elasticsearch"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Elasticsearch Aliases](https://www.objectrocket.com/blog/elasticsearch/elasticsearch-aliases/)

related
: [Elasticsearch]({{<relref "20201221151118-elasticsearch.md#" >}})


## Index Alias {#index-alias}

index alias di [Elasticsearch]({{<relref "20201221151118-elasticsearch.md#" >}}) bisa menunjuk ke sebuah index

hal ini bisa digunakan saat indexing, dan membuat proses index minim _downtime_

contohnya sbb

1.  asumsikan ada sebuah index yang disebut `customer_old` yang ingin di reindex
2.  buat sebuah alias `customers` yang menunjuk ke index `customer_old`
3.  pastikan aplikasi menggunakan index `customers`
4.  sementara itu buat index baru `customer_new`
5.  ketika proses indexing selesai tambahkan `customer_new` ke alias `customers`
6.  delete `customer_old`


## Example {#example}

```txt
POST /_aliases
{
    "actions": [
        { "remove": { "index": "my_index_v1", "alias": "my_index" }},
        { "add":    { "index": "my_index_v2", "alias": "my_index" }}
    ]
}
```

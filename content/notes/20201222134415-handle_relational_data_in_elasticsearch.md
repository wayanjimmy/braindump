+++
title = "Handle relational data in Elasticsearch"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Application Joins](https://www.elastic.co/guide/en/elasticsearch/guide/master/application-joins.html)

Q: How to handle relational data in [Elasticsearch]({{< relref "20201221151118-elasticsearch" >}})?
A: Salah satu caranya adalah join di application layers, dengan cara multi query.

Multi query maksudnya adalah melakukan query berkali-kali ke elastic search sesuai dengan data yang diperlukan, dan melakukan penggabungan data tersebut di layer aplikasi.

+++
title = "Immutable data elasticsearch"
author = ["Wayanjimmy"]
draft = false
+++

link
: [Belajar Elasticsearch - 9 Immutable Data](https://youtu.be/w-kv7ur253g?list=PL-CtdCApEFH%5FtVTwrxVt0K5LmtVT2u8fh)


## Immutable {#immutable}

-   dokumen yang ada di [Elasticsearch]({{< relref "20201221151118-elasticsearch" >}}) disimpan secara immutable di dalam disk
-   tidak akan pernah berubah selama-nya
-   benefitnya
    -   tidak perlu ada proses locking, seperti di RDBMS
    -   tidak perlu khawatir ada beberapa proses bersamaan yg mengakses atau mengubah potongan data yang sama


## Delete & Update {#delete-and-update}

-   karena immutable, proses update & delete sebenarnya tidak di update & delete sama sekali
-   setiap index memiliki file `.del`, yang berisikan daftar dokumen yang di hapus
-   ketika update dokumen, sebenarnya dokumen lama ditandai sebagai file yang di hapus dengan cara ditambahkan di file `.del`, dan perubahan yang baru disimpan sebagai dokumen baru.
-   secara reguler [Elasticsearch]({{< relref "20201221151118-elasticsearch" >}}) akan melakukan cleanup, data yg marked as delete nantinya akan di delete permanent.

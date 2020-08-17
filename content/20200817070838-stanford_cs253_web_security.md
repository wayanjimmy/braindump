+++
title = "Stanford CS253 Web Security"
author = ["Wayanjimmy"]
draft = false
+++

tags
: [Course]({{< relref "20200816205109-course" >}})


## Lecture 03: Session Attacks {#lecture-03-session-attacks}


### Sessions {#sessions}


#### Cookies diperlukan oleh server untuk implement sessions {#cookies-diperlukan-oleh-server-untuk-implement-sessions}


#### Session digunakan jika server ingin menyimpan data terkait user yang sedang melakukan sesi browsing {#session-digunakan-jika-server-ingin-menyimpan-data-terkait-user-yang-sedang-melakukan-sesi-browsing}

<!--list-separator-->

-  Sebagai contoh biasanya menyimpan aktivitas user yang sedang login

<!--list-separator-->

-  Contoh lain

    <!--list-separator-->

    -  Shopping cart

    <!--list-separator-->

    -  User tracking


#### Ambient Authority {#ambient-authority}

<!--list-separator-->

-  Meregulasi apa yang boleh dan tidak boleh diakses oleh requestor kepada server

<!--list-separator-->

-  Jenis ambient authority

    <!--list-separator-->

    -  Cookies - yang paling umum

    <!--list-separator-->

    -  IP checking

    <!--list-separator-->

    -  Built-in HTTP authentication - jarang digunakan

    <!--list-separator-->

    -  Client certificates - jarang digunakan


#### Solusi Keamanan Cookie {#solusi-keamanan-cookie}

<!--list-separator-->

-  Dengan sign cookie tersebut

<!--list-separator-->

-  Kita tidak bisa mempercayai browser

<!--list-separator-->

-  Jadi server harus memastikan kalau browser tidak mengubah nilai cookie yang udah diberikan


#### Gambaran cara kerja signing cookies {#gambaran-cara-kerja-signing-cookies}

<!--list-separator-->

-  ![](/ox-hugo/20200817154647-signing-cookies.png)

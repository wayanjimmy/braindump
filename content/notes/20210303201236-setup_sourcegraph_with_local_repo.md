+++
title = "Setup Sourcegraph with Local Repo"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Git]({{< relref "20210217134705-git" >}}) [Tinkering]({{< relref "20210503100841-tinkering" >}})


## Setup Sourcegraph Docker {#setup-sourcegraph-docker}

Siapkan machine linux yang akan digunakan sebagai tempat sourcegraph server, gunakan [Multipass]({{< relref "20210228151250-multipass" >}}) untuk launch vm ubuntu noconfig.
Pastikan docker sudah terinstall dan jalankan sourcegraph dengan metode [quick install](https://docs.sourcegraph.com/#quickstart-guide).

{{< figure src="/ox-hugo/multipass-sourcegraph.png" >}}

```bash
docker run -d --publish 7080:7080 --publish 127.0.0.1:3370:3370 --rm --volume ~/.sourcegraph/config:/etc/sourcegraph --volume ~/.sourcegraph/data:/var/opt/sourcegraph sourcegraph/server:3.25.2
```

Untuk membaca repository yang akan di-index, sourcegraph punya kemampuan untuk membaca code dari beberapa host yang berbeda seperti Git, Gitlab, you name it.
Namun aku berniat untuk meng-index repo yang sudah ada dilocal, disinilah peran [serve-git](https://docs.sourcegraph.com/admin/external%5Fservice/src%5Fserve%5Fgit).


## Install serve-git {#install-serve-git}

Install serve-git ikuti panduan [ini](https://github.com/sourcegraph/src-cli). Jika sudah jalankan di directory yang dinginkan

```bash
src serve-git
```

Buka lagi sourcegraph cari menu Site Admin &rarr; Manage Repositories &rarr; Add repositories &rarr; Sourcegraph CLI Serve-Git

masukan alamat IP tempat dijalankan serve-git di bagian url, contoh: <http://192.168.x.x:3434>

Di halaman repository status, jika muncul warning kalau repository sedang di clone, bisa diakalin dengan clone local repository.


## Menambahkan repository yang sudah di clone sebagai sumber index {#menambahkan-repository-yang-sudah-di-clone-sebagai-sumber-index}

Sourcegraph akan menyimpan repo git di host direktori ini `$HOME/.sourcegraph/data/repos`, nah jadi kita bisa clone git bare repository direktori ini

```bash
cd $HOME/.sourcegraph/data/repos
git clone --bare /alamat/ke/repo/yang/sudah/diclone $HOME/.sourcegraph/data/repos/nama_repo/.git
cd nama_repo
git fetch origin
#checkout juga ke beberapa branch yang diinginkan agar kode bisa di index
```

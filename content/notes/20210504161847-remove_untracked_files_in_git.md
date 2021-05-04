+++
title = "Remove Untracked Files in Git"
author = ["Wayanjimmy"]
draft = false
+++

link
: [How to remove untracked files in Git](https://linuxize.com/post/how-to-remove-untracked-files-in-git/)

related
: [Git]({{< relref "20210217134705-git" >}})

Sebelum membersihkan, konfirmasi dulu file yang akan di delete dengan flag `-n`

```bash
git clean -d -n
```

Outputnya akan seperti berikut

> Would remove content/test/
> Would remove content/blog/post/example.md

Kalau sudah yakin eksekusi perintah berikut

```bash
git clean -d -f
```

Check dengan perintah `git status`, working directory sekarang jadi bersih!

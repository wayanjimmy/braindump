+++
title = "Chezmoi for dotfiles management"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Tinkering](20210503100841-tinkering.md)

link
: [Chezmoi](https://github.com/twpayne/chezmoi)


## Init chezmoi {#init-chezmoi}

```bash
chezmoi init <remote_git_repo_url>
```


## Add file {#add-file}

```bash
chezmoi add ~/.vimrc
```


## Sync to remote git repository {#sync-to-remote-git-repository}

```bash
chezmoi cd

git add .

git commit -m "update"

git push
```


## Make changes to a file {#make-changes-to-a-file}

After you make changes to a tracked file

```bash
chezmoi add ~/.vimrc
```

and sync again to the remote repository

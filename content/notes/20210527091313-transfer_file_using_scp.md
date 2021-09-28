+++
title = "Transfer file using SCP"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Linux]({{<relref "20210502110347-linux.md#" >}})


link
: [How to use SCP commands to securely transfer files](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/)


## Upload file from host to a remote server {#upload-file-from-host-to-a-remote-server}

```bash
scp <file_name> remote_username@10.10.0.2:/remote/directory
```


## Upload directory from host to a remote server {#upload-directory-from-host-to-a-remote-server}

```bash
scp -r <file_name> remote_username@10.10.0.2:/remote/directory
```

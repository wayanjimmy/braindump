+++
title = "Generate mermaid diagrams using org mode"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Doom Emacs]({{< relref "20201208184126-doom_emacs" >}})

link
: [ob-mermaid](https://github.com/arnm/ob-mermaid)


Install package by adding line below to your `.doom.d/packages.el`

    ```elisp
       (package! ob-mermaid)
    ```


Install mermaid.cli locally.

    ```bash
       cd /to/your/org-roam-path
       yarn add mermaid.cli
    ```


Specify mmdc executable path

    ```elisp
       (setq ob-mermaid-cli-path "/your-installating-path/node_modules/.bin/mmdc")
    ```


open org-mode buffer and create a `org-babel` source block:

    ```nil
       #+begin_src mermaid :file filename.png
       sequenceDiagram
        A-->B: Works!
    ```

    \#+end\_src


Exporting the `org-mode` document or invoking the the `org-babel-execute-src-block` function to generate the diagram.

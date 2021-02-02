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

Install [mermaid.cli](https://github.com/mermaid-js/mermaid-cli) locally.

```bash
cd /to/your/org-roam-path
yarn add @mermaid-js/mermaid-cli
```

Specify mmdc executable path

```elisp
(setq ob-mermaid-cli-path "/your-installating-path/node_modules/.bin/mmdc")
```

Open `org-mode` buffer and create a `org-babel` source block:

{{< figure src="/ox-hugo/test.png" >}}

please note that you need to specify the `:file` header arguments, see this [issue](https://github.com/arnm/ob-mermaid/issues/9)

Exporting the `org-mode` document or invoking the the `org-babel-execute-src-block` function to generate the diagram.

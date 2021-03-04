+++
title = "Golang parse template from string and to string"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Golang]({{< relref "20201205165502-golang" >}})

<!--listend-->

```go
t, err := template.New("Test").Parse("Hello {{.Name}}, Good Morning!")
if err != nil {
	return err
}

data := struct{
	Name: string
}{
	Name: "Jimmy"
}
var tpl bytes.Buffer
err = t.Execute(&tpl, data)
if err != nil {
	return err
}

result = tpl.String()
```

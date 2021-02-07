+++
title = "Builder pattern in Golang"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Golang]({{< relref "20201205165502-golang" >}})

Sebuah pattern yg digunakan untuk mengkontruksi sesuatu, bisa sebuah string, struct ataupun closure.

Builder pattern cocok digunakan untuk mengkontruksi objek yang kompleks, jadi untuk menghindari bug yang terjadi saat proses kontruksi, dipecah jadi method method yang lebih mudah untuk digunakan.


## Contoh Builder Pattern {#contoh-builder-pattern}

```go
type Employee struct {
	Name string
	Role string
	MinSalary int
	MaxSalary int
}
```

Jika langsung melakukan kontruksi melalui struct diatas kita bisa saja lakukan dengan inisialisasi struct baru tersebut dan lakukan pengisian nilai ke masing-masing properti-nya.

```go
e := Employee{}
e.Name = "jimmy"
```

Namun kadang keperluan kita tidak sesederhana contoh diatas. Kadang ada kepentingan jika properti `Role` diisi nilai tetentu, kita ingin properti `MinSalary` atau `MaxSalary` diisi juga dengan nilai tertentu

```go
type Builder struct {
	e Employee
}

func (b *Builder) Build() Employee {
	return b.e
}

func (b *Builder) Name(name string) *Builder {
	b.e.Name = name
	return b
}

func (b *Builder) Role(role string) *Builder {
	if role == "manager" {
		b.e.MinSalary = 20000
		b.e.MaxSalary = 60000
	}
	b.e.Role = role
}

// cara mengkonstruksi struct Employee dengan Builder

b := &Builder{}
employee := b.
	Name("Jimmy").
	Role("manager").
	Build()

fmt.Println(employee)
```

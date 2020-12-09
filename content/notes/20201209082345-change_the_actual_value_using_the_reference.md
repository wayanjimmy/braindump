+++
title = "Change the actual value using the reference"
author = ["Wayanjimmy"]
draft = false
+++

related
: [Learn go with tests]({{< relref "20201208202033-learn_go_with_tests" >}})

Take a look at this piece of code

```go
func (f *FileSystemPlayerStore) RecordWin(name string) {
    league := f.GetLeague()

    for i, player := range league {
        if player.Name == name {
            league[i].Wins++
        }
    }

    f.database.Seek(0,0)
    json.NewEncoder(f.database).Encode(league)
}
```

You may be asking yourself why I am doing `league[i].Wins++` rather than `player.Wins++`

When you range over a slice you are returned the current index of the loop (in our case `i`) and a **copy** of the element at that index

We need to get the reference to the actual value by doing `league[i]` and then changing the value instead.

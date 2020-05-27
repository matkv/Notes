# Flow control

## If

There are no brackets around the condition.

```go
func main() {
    x := 7

    if x > 6 {
        fmt.Println("More than 6.")
    } else if x < 2 {
        //do something
    } else {
        //do something else
    }    
}
```

## Switch case

```go
switch condition {
    case example1:
        //do something
    case example2:
        //do domething else
    default:
        //this happens if none of the other options happened
}
```
# Go

[Go programming language tour](https://tour.golang.org/)

## Basics

### Packages

Every Go program is made up of packages. Programs start running in the package ```main```.

The package name is the same as the last element of the import path -> for example, the "math/rand" package includes files that begin with the statement ```package rand```.

### Imports

The ```import()``` method groups imports into one statement.

This:

```go
import (
	"fmt"
	"math"
)
```

Is the same as this:

```go
import "fmt"
import "math"
```

### Exported names

In Go, a name is **exported** if it begins with a capital letter.

When importing a package, we can only refer to its exported names. Any "unexported" names are not accessible from outside the package.

```go
func main() {
	fmt.Println(math.pi)	//this won't work
}

func main() {
	ftm.Println(math.Pi)	//this works
}
```

### Functions

A function can take zero or more arguments. In this example, ```add``` takes two parameters of type ```int```.

```go
func add(x int, y int) int {
	return x + y
}
```

The type comes *after* the variable name.

When two or more consecutive function parameters share a type, we can omit the type for all but the last:

```go
func add(x, y int) int {
	return x + y
}
```
### Return values

A function can return **multiple results**:

```go
func swap(x, y string) (string, string) {
	return y, x
}
```

A ```return``` statement without arguments returns the named return values. This is known as a ```naked``` return. Naked returns should only be used for short functions because they can harm readability:

```go
func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}
```

### Variables

The ```var``` statement declares (a list of) variables. This can be at package level or function level:

```go
package main

import "fmt"

var c, python, java bool

func main() {
	var i int
	fmt.Println(i, c, python, java)
}
```

Stopped at https://tour.golang.org/basics/9

## Methods and Interfaces

## Concurrency
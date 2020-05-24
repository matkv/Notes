# Go

[Go programming language tour](https://tour.golang.org/)

[Learn Go with tests](https://quii.gitbook.io/learn-go-with-tests/)

## Basics

### $GOPATH

By convention, all Go code lives within a single workspace (folder). Go places its files in three directories. In the directory of the `$GOPATH`, there are usually three directories:

* source code is in `scr`
* package objects are in `pkg`
* compiled programs are in `bin`

### Go modules

Go 1.11 introduced modules, enabling an alternative worklow which will deprecate the use of `GOPATH` and become the default mode. They enable users to run Go code outside of `GOPATH`.

We can select any directory outside `GOPATH` as the root of our project, and create a new module with the `go mod init` command.

```bash
go mod init example.com/m/v2
```

This will create a `go.mod` file. In order for the `go get` command to work (necessary to get packages and run tests), the folder in which we run the `go get` or `go test` commands needs to contain this `go.mod` file.

### Packages

Every Go program is made up of packages. Programs start running in the package ```main```.

The package name is the same as the last element of the import path -> for example, the "math/rand" package includes files that begin with the statement ```package rand```.

### Running a Go program

We can run a Go program using the `go run` command followed by the name of the go file.

If we want to compile the code into an executable, we run `go build` in the program's directory. This creates an executable binary file (for example an .exe file in Windows).

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

When importing a package, we can only refer to its exported names. Any "unexported" names are not accessible from outside the package. Exported symbols can be sued by other packages, unexported symbols cannot.

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

We can also include initializers, one per variable. If an initializer is present, the type can be omitted - the variable will take the type of the initializer.

```go
package main

import "fmt"

var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}
```

Inside a function, short way to declare a variable is the ```:=``` statement.

It can be used instead of ```var```. This is not possible outside a function.

```go
func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"

	fmt.Println(i, j, k, c, python, java)
}
```
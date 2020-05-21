# Types

Go's basic types are

```go
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

The `int`, `uint` and `uintptr` types are usually 32 bits wide on 32-bit systems and 64 bits wide on 64-bit systems. If we need an integer value we should use `int` unless we have a specific reason to use a sized or unsigned integer type.

# Zero values

Variables declared without an explicit initial value are given their `zero` value.

The zero value is:

* `0` for numeric types
* `false` for the boolean type
* `""` for strings

```go
package main

import "fmt"

func main() {
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}

```

This would print 0 0 false "".

# Type conversions

The expression `T(v)` converts the value `v` to the type `T`.

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```

Or:

```go 
i := 42
f := float64(i)
u := uint(f)
```

The assignment between items of different types requires an explicit conversion.

# Type inference

When declaring a variable without specifying  an explicit type the variable's type is inferred from the value on the right hand side.

When the right side of the declaration is `typed`, the new variable is of that same type:

```go
var i int
j := i // j is an int
```

But when the right hand side contains an `untyped` numeric constant, the new variable may be `int`, `float64` or `complex128` depending on the precision of the constant:

```go
i := 42           // int
f := 3.142        // float64
g := 0.867 + 0.5i // complex128
```

# Constants

Constants are declared like variables, but with the `const` keyword. They can be `character`, `string`, `boolean` or `numeric` values. They cannot be declared using the `:=` syntax.

```go
const Pi = 3.14
```

# Numeric constants

Numeric constants are high-precision *values*. An untyped constant takes the type needed by its context.

```go
package main

import "fmt"

const (
	// Create a huge number by shifting a 1 bit left 100 places.
	// In other words, the binary number that is 1 followed by 100 zeroes.
	Big = 1 << 100
	// Shift it right again 99 places, so we end up with 1<<1, or 2.
	Small = Big >> 99
)

func needInt(x int) int { return x*10 + 1 }
func needFloat(x float64) float64 {
	return x * 0.1
}

func main() {
	fmt.Println(needInt(Small))
	fmt.Println(needFloat(Small))
	fmt.Println(needFloat(Big))
}

```

# Arrays

We can initialise an array like this:

```go
var a [5]int    //creates an array with length 5
```

The values will all have the default zero value for the type - in this case, 

We can set a value like this: `a[2] = 7` or use the shorthand syntax:

```go
a := [5]int{5,4,3,2,1}
```

# Slices

If we don't want to have a specific length we must use, we can use `slices` instead of `arrays`.

We simply leave out the lenght:

```go
a := []int{5,4,3,2}
```

We can now also use the `append()` function to add values.

```go
a = append(a, 13)
```

# Maps

Maps hold key-value pairs (similar to dictionaries). To create a map, we use the built-in `make` function and give it this type.

```go
mapvalues := make(map[string]int)	//map with keys of type string and values of type int

mapvalues["firstvalue"] = 1
mapvalues["secondvalue"] = 2

fmt.Println(mapvalues)	//prints all values in the map
fmt.Println(mapvalues["firstvalue"])	//this prints 1

delete(mapvalues, "secondvalue")	//deletes the value
```

Stopped at 6:21 [Learn Go In 12 Minutes](https://www.youtube.com/watch?v=C8LgvuEBraI)
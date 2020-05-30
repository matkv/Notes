# Go Testing

To write a test for a function, we can use the VSCode command `Go: Generate unit tests for function` command.

Here is an example test that checks if a function returns "Hello world!".

```go
package main

import "testing"

func TestHello(t *testing.T) {
	got := Hello()
	want := "Hello world!"

	if got != want {
		t.Errorf("got %q want %q", got, want)
	}
}
```

Writing a test is just like writing a function, with a few rules:

* It needs to be in a file with a name that ends with `_test.go`.
* The test function must start with the word `Test`
* The test function takes one arument only `t *testing.T`

## t.Errorf

The `Errorf` method will print out a message and fail the test. The `f` stands for format which allows us to build a string with values inserted to the placeholder values `%q`.

## Writing tests

Usually we want to write tests first. For example, here is a test that cheks if our `Hello` function returns Hello followed by your name.

```go
package main

import "testing"

func TestHello(t *testing.T) {
	got := Hello("Matko")
	want := "Hello Matko!"

	if got != want {
		t.Errorf("got %q want %q", got, want)
	}
}
```

Here is an example where we run multiple tests depending on what input our `Hello` function gets:

```go
func TestHello(t *testing.T) {

	t.Run("saying hello to people", func(t *testing.T) {
		got := Hello("Matko")
		want := "Hello Matko!"

		if got != want {
			t.Errorf("got %q want %q", got, want)
		}
	})

	t.Run("say 'Hello World!' when an empty string is supplied", func(t *testing.T) {
		got := Hello("")
		want := "Hello World!"

		if got != want {
			t.Errorf("got %q want %q", got, want)
		}
	})
}
```

We can refactor this to use less duplicate code. In Go we can declare functions inside other functions and assign them to varaibles.

`t.Helper()` is needed to tell the test suite that this method is a helper. By doing this when it fails the line number reported will be in our *function call* rather than inside our test helper. This helps with tracking down the problem.

```go
package main

import "testing"

func TestHello(t *testing.T) {

	assertCorrectMessage := func(t *testing.T, got, want string) {
		t.Helper()
		if got != want {
			t.Errorf("got %q want %q", got, want)
		}
	}

	t.Run("saying hello to people", func(t *testing.T) {
		got := Hello("Matko")
		want := "Hello Matko!"

		assertCorrectMessage(t, got, want)
	})

	t.Run("say 'Hello World!' when an empty string is supplied", func(t *testing.T) {
		got := Hello("")
		want := "Hello World!"

		assertCorrectMessage(t, got, want)
	})
}

```

## Procedure of writing tests

* Write the test
* Make the compiler pass
* Run the test - it should fail and the error message should make sense
* Write enough code to make the test pass
* Refactor

## Adding an example

```go
func ExampleAdd() {
	sum := Add(1, 5)
	fmt.Println(sum)
	// Output: 6
}
```

By adding an example function to the test file **with** the comment inside the function makes it possible to access it in the documentation by running the `godoc` command. There it will show up under third party.
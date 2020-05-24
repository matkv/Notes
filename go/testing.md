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

Stopped at [https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/hello-world#t-errorf](https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/hello-world#t-errorf)
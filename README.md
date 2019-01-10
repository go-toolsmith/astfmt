[![Go Report Card](https://goreportcard.com/badge/github.com/go-toolsmith/astfmt)](https://goreportcard.com/report/github.com/go-toolsmith/astfmt)
[![GoDoc](https://godoc.org/github.com/go-toolsmith/astfmt?status.svg)](https://godoc.org/github.com/go-toolsmith/astfmt)
[![Build Status](https://travis-ci.org/go-toolsmith/astfmt.svg?branch=master)](https://travis-ci.org/go-toolsmith/astfmt)

# astfmt

Package astfmt implements ast.Node formatting with fmt-like API.

## Installation

```bash
go get github.com/go-toolsmith/astfmt
```

## Example

```go
package main

import (
	"go/token"
	"os"

	"github.com/go-toolsmith/astfmt"
	"github.com/go-toolsmith/strparse"
)

func Example() {
	x := strparse.Expr(`foo(bar(baz(1+2)))`)
	// astfmt functions add %s support for ast.Node arguments.
	astfmt.Println(x)                         // => foo(bar(baz(1 + 2)))
	astfmt.Fprintf(os.Stdout, "node=%s\n", x) // => node=foo(bar(baz(1 + 2)))

	// Can use specific file set with printer.
	fset := token.NewFileSet() // Suppose this fset is used when parsing
	pp := astfmt.NewPrinter(fset)
	pp.Println(x) // => foo(bar(baz(1 + 2)))
}
```

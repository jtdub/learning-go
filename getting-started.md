# Go: Getting Started

## What is Go good at?

### The Problem

* C++
  * Advantages
    * High Performance
    * Type Safety
  * Disadvantages
    * Slow compilation
    * Historically complex syntax
* Java
  * Advantages
    * Rapid compilation
    * Type safety
  * Disadvantages
    * Complicated ecosystem
* Python
  * Advantages
    * Ease of use
  * Disadvantages
    * Lack of type safety
    * Relatively slow
* Go
  * Fast compilation
  * Fully compiled
  * Strongly typed
  * Concurrent by default
  * Garbage collected
    * systematic recovery of pooled computer storage that is used by a program when that program no longer needs the storage. It's a automatic memory management feature.
  * Simplicity as a core value
  * Enhances maintainability by erroring on unused packages at compile time
  * whitespace isn't enforced, but it is strongly encouraged

### What is Go Good At?

* Types of common Go Applications
  * Web services
  * Web applications
  * Task automation
  * Machine learning

## Demo

* https://play.golang.org/

```go
package main

// This is an import block, it allows multiple packages to be imported without
// repeating the "import" keyword.
import (
				"fmt"
)
*/
The main function, when part of the main package, 
identifies the entry point of an application.
*/
func main() {
				fmt.PrintIn("Hello, world")
}
```

## Downloading and installing Go

* https://golang.org/dl/

  * Download the operating system appropriate image and install it.

* Mac OS install tips

  * go installs in `/usr/local/go`. You will need to set the PATH environment variable to know where to look for the go binary.

  ```bash
  jtdub@jamess-mbp learning-go % go version
  zsh: command not found: go
  
  jtdub@jamess-mbp learning-go % cat >> ~/.zshrc <<EOL
  heredoc> export GOPATH=/usr/local/go
  heredoc> export PATH=$PATH:$GOPATH/bin
  heredoc> EOL
  
  jtdub@jamess-mbp learning-go % cat ~/.zshrc
  export GOPATH=/usr/local/go
  export PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/Library/Apple/usr/bin:/usr/local/go/bin:/usr/local/go/bin
  
  jtdub@jamess-mbp learning-go % source ~/.zshrc
  
  jtdub@jamess-mbp learning-go % go version
  warning: GOPATH set to GOROOT (/usr/local/go) has no effect
  go version go1.15.3 darwin/amd64
  ```

  ## Invoking Go

  ```bash
  jtdub@jamess-mbp learning-go % go
  Go is a tool for managing Go source code.
  
  Usage:
  
  	go <command> [arguments]
  
  The commands are:
  
  	bug         start a bug report
  	build       compile packages and dependencies
  	clean       remove object files and cached files
  	doc         show documentation for package or symbol
  	env         print Go environment information
  	fix         update packages to use new APIs
  	fmt         gofmt (reformat) package sources
  	generate    generate Go files by processing source
  	get         add dependencies to current module and install them
  	install     compile and install packages and dependencies
  	list        list packages or modules
  	mod         module maintenance
  	run         compile and run Go program
  	test        test packages
  	tool        run specified go tool
  	version     print Go version
  	vet         report likely mistakes in packages
  
  Use "go help <command>" for more information about a command.
  
  Additional help topics:
  
  	buildconstraint build constraints
  	buildmode       build modes
  	c               calling between Go and C
  	cache           build and test caching
  	environment     environment variables
  	filetype        file types
  	go.mod          the go.mod file
  	gopath          GOPATH environment variable
  	gopath-get      legacy GOPATH go get
  	goproxy         module proxy protocol
  	importpath      import path syntax
  	modules         modules, module versions, and more
  	module-get      module-aware go get
  	module-auth     module authentication using go.sum
  	module-private  module configuration for non-public modules
  	packages        package lists and patterns
  	testflag        testing flags
  	testfunc        testing functions
  
  Use "go help <topic>" for more information about that topic.
  
  jtdub@jamess-mbp learning-go %
  ```

### Finding built-in documentation

The `go help <command>` is useful for finding documentation on go commands.

```bash
jtdub@jamess-mbp learning-go % go help doc
usage: go doc [-u] [-c] [package|[package.]symbol[.methodOrField]]

Doc prints the documentation comments associated with the item identified by its
arguments (a package, const, func, type, var, method, or struct field)
followed by a one-line summary of each of the first-level items "under"
that item (package-level declarations for a package, methods for a type,
etc.).

Doc accepts zero, one, or two arguments.

Given no arguments, that is, when run as

	go doc

it prints the package documentation for the package in the current directory.
If the package is a command (package main), the exported symbols of the package
are elided from the presentation unless the -cmd flag is provided.

When run with one argument, the argument is treated as a Go-syntax-like
representation of the item to be documented. What the argument selects depends
on what is installed in GOROOT and GOPATH, as well as the form of the argument,
which is schematically one of these:

	go doc <pkg>
	go doc <sym>[.<methodOrField>]
	go doc [<pkg>.]<sym>[.<methodOrField>]
	go doc [<pkg>.][<sym>.]<methodOrField>

The first item in this list matched by the argument is the one whose documentation
is printed. (See the examples below.) However, if the argument starts with a capital
letter it is assumed to identify a symbol or method in the current directory.

For packages, the order of scanning is determined lexically in breadth-first order.
That is, the package presented is the one that matches the search and is nearest
the root and lexically first at its level of the hierarchy. The GOROOT tree is
always scanned in its entirety before GOPATH.

If there is no package specified or matched, the package in the current
directory is selected, so "go doc Foo" shows the documentation for symbol Foo in
the current package.

The package path must be either a qualified path or a proper suffix of a
path. The go tool's usual package mechanism does not apply: package path
elements like . and ... are not implemented by go doc.

When run with two arguments, the first must be a full package path (not just a
suffix), and the second is a symbol, or symbol with method or struct field.
This is similar to the syntax accepted by godoc:

	go doc <pkg> <sym>[.<methodOrField>]

In all forms, when matching symbols, lower-case letters in the argument match
either case but upper-case letters match exactly. This means that there may be
multiple matches of a lower-case argument in a package if different symbols have
different cases. If this occurs, documentation for all matches is printed.

Examples:
	go doc
		Show documentation for current package.
	go doc Foo
		Show documentation for Foo in the current package.
		(Foo starts with a capital letter so it cannot match
		a package path.)
	go doc encoding/json
		Show documentation for the encoding/json package.
	go doc json
		Shorthand for encoding/json.
	go doc json.Number (or go doc json.number)
		Show documentation and method summary for json.Number.
	go doc json.Number.Int64 (or go doc json.number.int64)
		Show documentation for json.Number's Int64 method.
	go doc cmd/doc
		Show package docs for the doc command.
	go doc -cmd cmd/doc
		Show package docs and exported symbols within the doc command.
	go doc template.new
		Show documentation for html/template's New function.
		(html/template is lexically before text/template)
	go doc text/template.new # One argument
		Show documentation for text/template's New function.
	go doc text/template new # Two arguments
		Show documentation for text/template's New function.

	At least in the current tree, these invocations all print the
	documentation for json.Decoder's Decode method:

	go doc json.Decoder.Decode
	go doc json.decoder.decode
	go doc json.decode
	cd go/src/encoding/json; go doc decode

Flags:
	-all
		Show all the documentation for the package.
	-c
		Respect case when matching symbols.
	-cmd
		Treat a command (package main) like a regular package.
		Otherwise package main's exported symbols are hidden
		when showing the package's top-level documentation.
	-short
		One-line representation for each symbol.
	-src
		Show the full source code for the symbol. This will
		display the full Go source of its declaration and
		definition, such as a function definition (including
		the body), type declaration or enclosing const
		block. The output may therefore include unexported
		details.
	-u
		Show documentation for unexported as well as exported
		symbols, methods, and fields.
```

The `go doc` command is useful for finding documentation strings in code.

```bash
jtdub@jamess-mbp learning-go % go doc json.Decoder.Decode
warning: GOPATH set to GOROOT (/usr/local/go) has no effect
package json // import "encoding/json"

func (dec *Decoder) Decode(v interface{}) error
    Decode reads the next JSON-encoded value from its input and stores it in the
    value pointed to by v.

    See the documentation for Unmarshal for details about the conversion of JSON
    into a Go value.

jtdub@jamess-mbp learning-go % go doc json.Decoder
warning: GOPATH set to GOROOT (/usr/local/go) has no effect
package json // import "encoding/json"

type Decoder struct {
	// Has unexported fields.
}
    A Decoder reads and decodes JSON values from an input stream.

func NewDecoder(r io.Reader) *Decoder
func (dec *Decoder) Buffered() io.Reader
func (dec *Decoder) Decode(v interface{}) error
func (dec *Decoder) DisallowUnknownFields()
func (dec *Decoder) InputOffset() int64
func (dec *Decoder) More() bool
func (dec *Decoder) Token() (Token, error)
func (dec *Decoder) UseNumber()
jtdub@jamess-mbp learning-go % go doc json
warning: GOPATH set to GOROOT (/usr/local/go) has no effect
package json // import "encoding/json"

Package json implements encoding and decoding of JSON as defined in RFC
7159. The mapping between JSON and Go values is described in the
documentation for the Marshal and Unmarshal functions.

See "JSON and Go" for an introduction to this package:
https://golang.org/doc/articles/json_and_go.html

func Compact(dst *bytes.Buffer, src []byte) error
func HTMLEscape(dst *bytes.Buffer, src []byte)
func Indent(dst *bytes.Buffer, src []byte, prefix, indent string) error
func Marshal(v interface{}) ([]byte, error)
func MarshalIndent(v interface{}, prefix, indent string) ([]byte, error)
func Unmarshal(data []byte, v interface{}) error
func Valid(data []byte) bool
type Decoder struct{ ... }
    func NewDecoder(r io.Reader) *Decoder
type Delim rune
type Encoder struct{ ... }
    func NewEncoder(w io.Writer) *Encoder
type InvalidUTF8Error struct{ ... }
type InvalidUnmarshalError struct{ ... }
type Marshaler interface{ ... }
type MarshalerError struct{ ... }
type Number string
type RawMessage []byte
type SyntaxError struct{ ... }
type Token interface{}
type UnmarshalFieldError struct{ ... }
type UnmarshalTypeError struct{ ... }
type Unmarshaler interface{ ... }
type UnsupportedTypeError struct{ ... }
type UnsupportedValueError struct{ ... }
jtdub@jamess-mbp learning-go %
```

## Visual Studio Code Setup


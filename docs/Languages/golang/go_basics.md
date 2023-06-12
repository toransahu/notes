# Golang Basics

[TOC]

# Introduction

- intially developed at Google - 2007
- by Robert Griesemer, Rob Pike, and Ken Thompson
- is a statically-typed language with syntax similar to that of C
- provides
    - garbage collection
    - type safety
    - dynamic-typing capability
    - many advanced built-in types such as
        - variable length arrays
        - key-value maps
        - heap
    - a rich standard library
- is expressive, concise, clean, and efficient
- its concurrency mechanisms make it easy to write programs that get the most out of multi core and networked machines
- compiles quickly to machine code yet has the convenience of garbage collection and the power of run-time reflection
    - [runtime reflection in go](https://blog.golang.org/laws-of-reflection)
    - [garbage collection in go](https://blog.golang.org/ismmkeynote)

# How Go is different than other languages

- native concurrency support - i.e. at language-level
- different GC design
- single executable - copy/paste & deploy
- no dynamic/linked libraries
- keep lang. simple & expressive
- directly compiles to `machine code` - no virtual runtime or interpreter concept
- `interior pointer` concept

# Install

# Setup

# Run

# Memory Management

- https://deepu.tech/memory-management-in-golang/
- https://medium.com/eureka-engineering/understanding-allocations-in-go-stack-heap-memory-9a2631b5035d

## Stack vs Heap

- https://stackoverflow.com/questions/10866195/stack-vs-heap-allocation-of-structs-in-go-and-how-they-relate-to-garbage-collec

## Garbage Collection

- https://blog.golang.org/ismmkeynote
- https://golang.org/doc/faq#garbage_collection

# Keywords

## `package`

## `import`

## `type`

## `const`

## `var`

## `func`

## `struct`

# Declaration

# Data Type

## `bool`

## `int`

## `string`

- https://blog.golang.org/strings
- In Go, a string is in effect a read-only slice of bytes
- string holds arbitrary bytes
    - It is not required to hold Unicode text, UTF-8 text, or any other predefined format
- string literal that uses \xNN notation to define a string constant holding some peculiar byte values
    - Of course, bytes range from hexadecimal values 00 through FF, inclusive

```go
const sample = "\xbd\xb2\x3d\xbc\x20\xe2\x8c\x98"
fmt.Println(sample) // out: ��=� ⌘
//  in our sample string are not valid ASCII, not even valid UTF-8, printing the string directly will produce ugly output
```

- _NOTE_: indexing/iterating over string gives bytes and not characters in Go
- that also means, when we store a character in a string, we store its byte representation

### UTF-8 and string literals

- placeOfInterest = `⌘`
  - Unicode character value U+2318

```go
const placeOfInterest = `⌘`

fmt.Printf("%s", placeOfInterest) // plain string: ⌘

fmt.Printf("%+q", placeOfInterest) // quoted string: "\u2318"

for i := 0; i < len(placeOfInterest); i++ {
    fmt.Printf("%x ", placeOfInterest[i])  // hex bytes: e2 8c 98
}

```

- _NOTE_:
    - Source code in Go is defined to be UTF-8 text; no other representation is allowed


## `byte`

## Code points, characters, and runes

- https://blog.golang.org/strings

Given

- lower case Latin letter 'A': a
    - A: unicode code point: U+0061
- lower case grave-accented letter 'A', à
    - B: unicode code point: U+00E0
- grave accent code point (that sign above a):
    - C: unicode code point: U+0300

Then  
 à == A + C
or à == B

- code point == rune
    - code point is a bit of mouthful, hence go introduces shorter term `rune`
    - rune meaning: any of the characters of any of several alphabets
- character

    - when we store a character value in a string, we store its byte-at-a-time representation
    - In general, a character may be represented by a number of different sequences of code points, and therefore different sequences of UTF-8 bytes
    - The concept of character in computing is therefore ambiguous, or at least confusing, so we use it with care

- _NOTE_:
    - Go team have been very careful so far in how we use the words "byte" and "character"
    - That's partly because strings hold bytes, and partly because the idea of "character" is a little hard/ambiguous to define

# Data Structure

## Array

```go
var a [5]int
fmt.Println("emp:", a)
a[4] = 100
fmt.Println("set:", a)
fmt.Println("get:", a[4])
```

## Slice

```go
s := make([]string, 3)
fmt.Println("emp:", s)

s[0] = "a"
s[1] = "b"
s[2] = "c"
fmt.Println("set:", s)

fmt.Println("get:", s[2])

fmt.Println("len:", len(s))

s = append(s, "d")
s = append(s, "e", "f")

c := make([]string, len(s))
copy(c, s)

l := s[2:5]

t := []string{"g", "h", "i"}

// TODO: len vs size??
```

## Map

```go
m := make(map[string]int)

m["k1"] = 7
v1 := m["k1"]

fmt.Println("len:", len(m))

delete(m, "k2")  // no error

isThere, value := m["k2"] // out: false, 0
isThere, value := m["k1"] // out: true, 7

n := map[string]int{"foo": 1, "bar": 2}
n := map[string]interface{}{"foo": 1, "bar": "some string"}
```

# Types & interfaces

- Go is statically typed
- Every variable has a static type, that is, exactly one type known and fixed at compile time: int, float32, \*MyType, []byte, and so on
- `interface` is one important category of type - which represent fixed/minimal sets of methods

If we declare

```go
type MyInt int

var i int
var j MyInt
```

then

- `i` has type `int` and `j` has type `MyInt`
- variables `i` and `j` have distinct static types and, although they have the same underlying type, they cannot be assigned to one another without a conversion

An interface variable can store any concrete (non-interface) value as long as that value implements the interface's methods.

```go
var r io.Reader
r = os.Stdin
r = bufio.NewReader(r)
r = new(bytes.Buffer)
// and so on
```

Here `r` can exhibit lot more methods than `Read()` of `io.Reader`. Its not limited to methods provided by interface `io.Reader`.

An extremely important example of an interface type is the empty interface: `interface{}`

## `interface{}`

A.K.A. Empty Interface

It represents the empty set of methods and is satisfied by any value at all, since any value has zero or more methods.

- interface{} (empty interface) type describes an interface with zero methods
- Every Go type implements at least zero methods
    - therefore satisfies the empty interface
- so we can receive any go data type in an empty interface (similar to object/var in other langs.)

```
var i interface{}
i = "a string"
i = 2011
i = 2.777

fmt.Println()
```

- https://github.com/toransahu/go-misc/blob/master/interfac/main.go

A variable of interface type always has the same static type, and even though at run time the value stored in the interface variable may change type, that value will always satisfy the interface.

## The representation of an interface

- A variable of type `interface` type stores a pair: a concrete value assigned to the variable, and that concrete values's type/type-descriptor.

e.g.

```go
var r io.Reader
tty, err := os.OpenFile("/dev/tty", os.O_RDWR, 0)
if err != nil {
    return nil, err
}
r = tty
```

here `r` contains pair (value, concrete type) == (tty, \*os.File).

As a interface variable also stores the type details, we can do things like this:

```go
var w io.Writer
w = r.(io.Writer) // The expression in this assignment is a type assertion
// it asserts is that the item inside r also implements io.Writer, and so we can assign it to w

// or
var s interface{}
s = "hello"
ss := s.(string) // The expression in this assignment is a type assertion

// or

ss, ok := s.(string)
```

this is called `type assertion`.

# Reflection

- Reflection in computing is the ability of a program to examine its own structure, particularly through types; it's a form of metaprogramming. It's also a great source of confusion.
- reflection builds on the type system

## The first law of reflection - Reflection goes from interface value to reflection object

- At the basic level, reflection is just a mechanism to examine the type and value pair stored inside an interface variable
- there are two types we need to know about in package reflect: Type and Value
    - Those two types give access to the contents of an interface variable, and two simple functions, called `reflect.TypeOf()` and `reflect.ValueOf()`
    - tbd

## The second law of reflection - Reflection goes from reflection object to interface value

tbd

## The third law of reflection - To modify a reflection object, the value must be settable

tbd

# Statements

## Control Flows

### `if`, `else`

```go
if num := 9; num < 0 {
    fmt.Println(num, "is negative")
} else if num < 10 {
    fmt.Println(num, "has 1 digit")
} else {
    fmt.Println(num, "has multiple digits")
}
```

- _NOTE_: there is no ternary `?` if else condition

### `for`

- `for` is the only looping construct in Go
- `for` have 3-4 pattern

```go

// like while loop
i := 1
for i <= 3 {
    fmt.Println(i)
    i = i + 1
}

// regular for loop
for j := 7; j <= 9; j++ {
    fmt.Println(j)
}

for n := 0; n <= 5; n++ {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }

// infinite loop (or with break
for {
    fmt.Println("loop")
    break
}
```

### `switch`

```go

// regular switch case
i := 2
fmt.Print("Write ", i, " as ")
switch i {
case 1:
    fmt.Println("one")
case 2:
    fmt.Println("two")
case 3:
    fmt.Println("three")
}

// TODO:
switch time.Now().Weekday() {
case time.Saturday, time.Sunday:
    fmt.Println("It's the weekend")
default:
    fmt.Println("It's a weekday")
}

// regular if else
t := time.Now()
switch {
case t.Hour() < 12:
    fmt.Println("It's before noon")
default:
    fmt.Println("It's after noon")
}

// interface type assertion
whatAmI := func(i interface{}) {
    switch t := i.(type) {
    case bool:
        fmt.Println("I'm a bool")
    case int:
        fmt.Println("I'm an int")
    default:
        fmt.Printf("Don't know type %T\n", t)
    }
}
whatAmI(true)
whatAmI(1)
whatAmI("hey")
```

### `goto`

- why its still valid in a new-gen prog. lang. ??

## `range`

```go
nums := []int{2, 3, 4}
sum := 0

// range on arrays and slices provides both the index and value for each entry
for _, num := range nums {
    sum += num
}

for i, num := range nums {
    if num == 3 {
        fmt.Println("index:", i)
    }
}

// range on map iterates over key/value pairs
kvs := map[string]string{"a": "apple", "b": "banana"}
for k, v := range kvs {
    fmt.Printf("%s -> %s\n", k, v)
}

// range can also iterate over just the keys of a map
for k := range kvs {
    fmt.Println("key:", k)
}

// range on strings iterates over Unicode code points
// The first value is the starting byte index of the rune and the second the rune itself.
for i, c := range "go" {
    fmt.Println(i, c)
}
// out:
0 103
1 111
```

# Functions

- src:
    - https://golang.org/doc/codewalk/functions/

## First Class

## User-defined

## Higher-order

- a function which accepts another function as a arg

## Closures

- a concept of having access of outer scope
- in an Anonynous function, `function literals` are closures: they inherit the scope of the function in which they are declared
- same as python, javascript

## Multiple Return Values

- similar to pl/sql procedures

```go
func() string, int { return "Yes", 1}
```

## Variadic

- variable/arbitrary numbers of arguments
- similar to `*args`
- `variable` [space] `...` concateanted to `type`
- `vardiac` arg is always a `slice`
- builtin e.g.
    - `fmt.Println`

```go
func sum(nums ...int) int {
    total := 0
    for _, number := range nums {
        total += number
    }
    return total
}

func main() {
    sum(1,2)
    sum(1,2,3)
}
```

- can directly pass a `slice` like

```go
num_slice := []int{1,2,3}
sum(num_slice ...)
```

## Anonymous/Lambda

```go
func(msg string) {
    fmt.Println(msg)
}("Some message")
```

## Access Modifier

- depends on CASE of the func
    - if starts with Capital case --> Public
        - should have comment/doc string
    - else private

# Struct

- regular struct
- in go, struct are alternative to classes

```go
type Vehicle struct {
    Make string  `json:make`  // additional json tag for de/serialization
    Fuel string
    Engine Engine
    owner string // not an exportable/exposed/public key/object
}

type Engine struct {
    Stroke string
    HorsePower string
}
```

## Methods

```go
func (v *Vehicle) Start() (string, error) {
    return "Vrooom", nil
}

engine := Engine{"Four", "1000"}
car := Vehicle{"Tesla", "Li", engine, "Toran"}
res, err := car.Start()
```

# Interface

- Interfaces are named collections of method signatures
- https://gobyexample.com/interfaces

# Constructor

# goroutine

- A goroutine is a lightweight thread of execution

## `go`

```go
func f(from string) {
    for i := 0; i < 3; i++ {
        fmt.Println(from, ":", i)
    }
}

func main() {
    f("direct")  // direct call

    go f("goroutine")  // goroutine call

    go func(msg string){
        fmt.Println(msg)
    }("goroutine from anonymous func")

    fmt.Scanln() // input from stdio

    fmt.Println("done")
}

// out:
direct : 0
direct : 1
direct : 2
goroutine : 0
goroutine from anonymous func
goroutine : 1
goroutine : 2
<enter>
done
```

by going through above mentioned example:

- if we want to invoke the function `f` as a goroutine we call it using `go` statement
    - func `f` will execute concurrently with the calling/main one
- we can also start a goroutine for an anonymous func
- our two function calls are running asynchronously in separate goroutines now
- we see output of
    - blocking/synchronous call first
    - then the interleaved output of two goroutines (output order may vary system to system)

## `defer`

tbd

- https://blog.golang.org/defer-panic-and-recover

## `panic`

## `recover`

## goroutine vs threads
- can run more number of goroutines on a typical system than can threads
- goroutine are managed by go runtime, and have been designed to be lightweight
    - thus the startup time is low
    - its lightweight because it gets assigned very minimal memory, and that could be increased on demand
        - that called growable segmented stack
-  goroutine comes with in-built primitives called `channels` to communicate safely between themselves
-  goroutines are multiplexed onto a small number of OS threads, rather than 1:1 mapping


# Channels

- https://gobyexample.com/channels
- Channels are the pipes that connect concurrent goroutines
    - You can send values into channels from one goroutine and receive those values into another goroutine

```go
messages := make(chan string) // create a channel named message
go func() { messages <- "ping" }() // from go routine `send` a string value/msg "ping" to the channel
msg := <-messages // `receive` value/msg from the channel
fmt.Println(msg)
fmt.Println(msg.(string) // assert type
```

- _NOTE_: By default sends and receives block until both the sender and receiver are ready. This property allowed us to wait at the end of our program for the "ping" message without having to use any other synchronization.
    - meaning that, whenever there will be receiver (and is ready to receive the value) then only sender can send the value/msg to the channel
    - see: https://github.com/toransahu/go-misc/blob/master/goroutines/channels/channels.go#L30
    - hence we can say, by default go channels are _unbufferred_

## Channel Buffering

- we checked above _NOTE_ about readiness of `senders` & `receivers`
    - channel buffering is to alter that nature & keep the value/msg in the buffer
- Buffered channels accept a limited number of values without a corresponding receiver for those values

```go
message := make(chan string, 2) // here 2 is capacity of the buffer
message <- "value 1"
message <- "value 2"
fmt.Println(<-message)
fmt.Println(<-message)
```

- https://github.com/toransahu/go-misc/blob/master/goroutines/channels/buffered/buffered_channels.go

## Channel Synchromization

tbd

- https://gobyexample.com/channel-synchronization

## Channel Directions

tbd

- https://gobyexample.com/channel-directions

## `select`

tbd

- https://gobyexample.com/select

### Timeouts

tbd

- https://gobyexample.com/timeouts

### Non-blocking Channel operations

tbd

- https://gobyexample.com/non-blocking-channel-operations

## Closing Channels

tbd

- https://gobyexample.com/closing-channels

## `range` over channels

tbd

- https://gobyexample.com/range-over-channels

# Modules

A module is a collection of related Go packages that are versioned together as a single unit.

Ref:

- https://github.com/golang/go/wiki/Modules#modules
- https://github.com/golang/go/wiki/Modules

## `go mod`

- to manage [versioned] dependencies
- was out with go 1.11 with preliminary/provisionary support & target to finalizing the feature for 1.14 (considering all feedbacks since 1.11-1.13)
- don't need to live the code in GOPATH
- creates/uses go.mod file
- the initial prototype `vgo` was announced in February 2018
- other alternatives were: dep, gom etc.
- management of interdependencies:
    - vgo's controversial algo uses the oldest common version to support stability
        - this may while discard the acceptance of any security bug fixed in newer version
    - e.g.
        - package A uses B and B uses D's atleast 1.0 version
        - package A also uses C and C uses D's either 1.0 or 1.1 version
        - then, as per vgo
- vgo
    - versioned go
    - manages all the algorithm of versioning the go projects/packages/modules
    - cmd `vgo build` is capable of generating go.mod
    - creates/manages versioned cache packages inside GOPATH/src/v
- there are support for more than one module in repository, but general idea is one
- As of Go 1.11, the go command enables the use of modules when the current directory or any parent directory has a go.mod, provided the directory is outside GOPATH/src. (Inside GOPATH/src, for compatibility, the go command still runs in the old GOPATH mode, even if a go.mod is found. See the go command documentation for details.)
- Starting in Go 1.13, module mode will be the default for all development.
- In addition to go.mod, the go command maintains a file named go.sum containing the expected cryptographic hashes of the content of specific module versions
    - to maintain the intigrity of the go.mod

### Semantic Import Versioning (SEMVER)

- way to handle major dependency changes like:
    - v1 to v2, v3,...
    - API/interface changes
- how
    - /github.com/toransahu/log (contains all v1.x.x) & /github.com/toransahu/log/v2 (contains all v2.x.x)

Ref:

- https://research.swtch.com/vgo-import

# Package

## main

## `package` Vs `directory`

## Built-in Packages

### `timer` & `ticker`

tbd

- https://gobyexample.com/timers
- https://gobyexample.com/tickers

continue exploring other packages from here

# Import

## Inbuilt Package

## Intra Package

## Inter Package

## Remote Package

## Cyclic

# `json`

## Encoding

- `func Marshal(v interface{}) ([]byte, error)`
- Only data structures that can be represented as valid JSON will be encoded:

    - JSON objects only support strings as keys; to encode a Go map type it must be of the form map[string]T (where T is any Go type supported by the json package).
    - TODO: Channel, complex, and function types cannot be encoded.
    - TODO: Cyclic data structures are not supported; they will cause Marshal to go into an infinite loop.
    - Pointers will be encoded as the values they point to (or 'null' if the pointer is nil)

- The json package only accesses the exported fields of struct types (those that begin with an uppercase letter). Therefore only the the exported fields of a struct will be present in the JSON output.
    - TODO: what if alias is also provided?
- we can also provide `json:"alias"` for each field in the struct
    - so that those fields will be encoded as per `aliases`
    - shortcut to generate those:
        - vim-go:
            - visual select -> `<leader> GoAddTags`
        - GoLand:

```go
// data structure, Message
type Message struct {
    Name string    `json:"name"`
    Body string    `json:"body"`
    Time int64     `json:"time"`
}

// an instance of Message
m := Message{"Alice", "Hello", 1294706395881547000}

// encoding m
b, err := json.Marshal(m)

// If all is well, err will be nil and b will be a []byte containing this JSON data
b == []byte(`{"Name":"Alice","Body":"Hello","Time":1294706395881547000}`)
```

- https://github.com/toransahu/go-misc/blob/master/json/encoding.go

## Decoding

- https://github.com/toransahu/go-misc/blob/master/json/decoding.go

## Generic JSON with interface{}

- The json package uses map[string]interface{} and []interface{} values
    - to store arbitrary JSON objects and arrays
- it will happily unmarshal any valid JSON blob into a plain interface{} value
- default concrete Go types are:
    - `bool` for JSON booleans
    - `float64` for JSON numbers
    - `string` for JSON strings
    - `nil` for JSON null

### Creating arbitrary data

```go
i := map[string]interface{}{"id": 1111, "name": "Toran"}
	fmt.Println(i)
}
```

### Encoding arbitrary data

```go
bytes := json.Marshal(i)
```

### Decoding arbitrary data

- https://github.com/toransahu/go-misc/blob/master/json/json_test.go#L33

```go
var i interface{}
json.Unmarshal(bytes, &i)
```

### Json & Reference Type (pointers, slices, maps)

- https://blog.golang.org/json-and-go
- https://github.com/toransahu/go-misc/blob/master/jsons/reference_type.go#L53

### Streaming Encoders and Decoders

- https://blog.golang.org/json-and-go

### Misc

- https://vsupalov.com/go-json-omitempty/
- https://www.reddit.com/r/golang/comments/k0hitv/compiler_written_in_go/
- [Lexical Scanning in Go - Rob Pike](https://www.youtube.com/watch?v=HxaD_trXwRE)

# `regexp`

Ref:

- https://golang.org/pkg/regexp/
- https://github.com/google/re2/wiki/Syntax
- https://shapeshed.com/golang-regexp/

# Errors

- https://gobyexample.com/errors

## Error Handling

- https://blog.golang.org/error-handling-and-go

# Testing

- test module should named as `*_test.go` under packages
- FIXME: better to organize test modules in a separate package - similar to Java??

## `Testcase`

## `Benchmarks`

## `Examples`

## `Skipping`

## `Subtests` and `Sub-benchmarks`

## `Main`

## Run

- a test file

  > ~/go/src/github.com/toransahu/go-misc/json on `` master! ⌚ 14:18:45  
  > &#36; go test json_test.go config.go encoding.go
  > ok command-line-arguments 0.003s

- all test files under a package

  > ~/go/src/github.com/toransahu/go-misc/json on `` master! ⌚ 14:18:56  
  > &#36; go test  
  > PASS  
  > ok github.com/toransahu/go-misc/json 0.002s

- all test files in all packages

  > tbd

- specific test function of a test file

  > tbd

- specific test function/file with pattern/regex
  > tbd

## Coverage

- https://blog.alexellis.io/golang-writing-unit-tests/

- src:
    - https://golang.org/pkg/testing/#hdr-Subtests_and_Sub_benchmarks
    - https://stackoverflow.com/questions/16935965/how-to-run-test-cases-in-a-specified-file

# Debug

## gdb

- https://golang.org/doc/gdb

## Delve

# Profiling

## `pprof`

- https://blog.golang.org/pprof

## CPU Profiling - stack sampling (vs instrumentation)

## Heap Profiling - allocation profiling

## Block

## Trace

# Deploy

## CircleCI

### Run Test

# Misc

## `generate`

- automatically generate golang code for a particular purpose
    - like print name of memebers in a struct
        - `stringr`
- https://blog.golang.org/generate
- can set header/preprocessor (with commands) in the go file to do the job on each build

## Advance Testing

### `assert`

- 3rd party packages for assert.\*
- https://github.com/stretchr/testify

## Extra

- https://talks.golang.org/2012/10things.slide#3

# Best Practices

## Naming Convetions

- https://golang.org/doc/effective_go.html#names
- https://blog.golang.org/package-names

## Code Organization

- Package
- main
- test
- https://blog.golang.org/organizing-go-code
- inside a directory
    - all modules with only single package name
- can only execute/run `main` package module
    - hence `main` package
- `func main` should be declared to run the `main` package module

# Documentation

- to document a type, variable, constant, function, or even a package, write a regular comment directly preceding its declaration, with no intervening blank line
- a complete sentence
- begins with the name of the element
- similar to `python`'s `Docstring` & `java`'s `Javadoc` but simpler than them
- src:
    - https://blog.golang.org/godoc-documenting-go-code

```go
// Package sort provides primitives for sorting slices and user-defined
// collections.
package sort

...

// Fprint formats using the default formats for its operands and writes to w.
// Spaces are added between operands when neither is a string.
// It returns the number of bytes written and any write error encountered.
func Fprint(w io.Writer, a ...interface{}) (n int, err error) {
```

- extra:
    - do something like [this](https://golang.org/src/encoding/gob/doc.go) to achieve [this](https://golang.org/pkg/encoding/gob/)
- notable keywords:
    - `Deprecated:`
    - `BUG(<contact person>)`

## `Godoc`

# Best Practices

# Concepts

## Compilation

## Static Typing

## Pointer

## Garbage Collection

- Go language features, goals, and use cases have forced to rethink the entire garbage collection stack and have led to a surprising place
- Go programs have hundreds of thousands of stacks
    - They are managed by the Go scheduler and are always preempted at GC safepoints
    - The Go scheduler multiplexes Go routines onto OS threads which hopefully run with one OS thread per HW thread
    - We manage the stacks and their size by copying them and updating pointers in the stack. It's a local operation so it scales fairly well.

Ref:

- https://blog.golang.org/ismmkeynote
- https://www.ardanlabs.com/blog/2018/12/garbage-collection-in-go-part1-semantics.html

# Debugging

## `gdb`
- https://golang.org/doc/gdb
- https://astaxie.gitbooks.io/build-web-application-with-golang/content/en/11.2.html

## Delve

# Profiling

- https://blog.golang.org/pprof

# Design Patterns

- [Functional options for friendly APIs](https://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis)
    - [Self referential functions and design](https://commandcenter.blogspot.com/2014/01/self-referential-functions-and-design.html)


# References

- https://golang.org/doc/code.html
- https://github.com/golang/go/wiki/Learn
- https://go.dev/about/#best-practices-h2

# Surprises

- https://medium.com/@karel_3d/things-that-surprised-me-in-go-47bccce94558
- https://utcc.utoronto.ca/~cks/space/blog/programming/GoInteriorPointerGC
- https://dave.cheney.net/2017/04/29/there-is-no-pass-by-reference-in-go

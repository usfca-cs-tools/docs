# Coding Style in Go

1. Go is [opinionated](https://go.dev/doc/effective_go#formatting) about stylistic elements, and some of those opinions are enforced by the `go fmt` formatter.
1. The central idea is that consistent coding style contributes to readability of code, even if individual programmers would prefer different choices.
1. Here are some basics to get CS 272 students started with Go, and understand the code you'll see.

## Braces and Spaces

1. Go uses tab characters for indentation and spaces for alignment
1. Go puts opening braces on the end of a line of code like this
    ```go
    if x == y {
        doSomething()
    }
    ```
    This is illegal syntax:
    ```go
    if x == y 
    {
        doSomething()
    }
1. Braces are always required around a block, unlike C which supports single-line blocks

## Optional Syntax

1. Semicolons are optional
1. Parens around `if` and `switch` conditions are optional

## Case

1. Go uses "camel case" names, such as `doSomething()` not "snake case" names, such as `do_something()`
1. Case also controls the scope of a name. An upper-case name is "exported" outside of a source code file, but a lower-case name is not
1. This can be very important when naming structure elements
    ```go
    type struct Foo {
        Count int
    }
    ```
    means that Foo and its Count element are exported
    ```go
    type struct Foo {
        Count        int
        privateCount int
    }
    ```
    means that `privateCount` is not exported, and not referenceable in source code outside the source file where it's declared.
1. Therefore, Go uses case to do what Java/C++ keywords like `public` and `private` do
1. Notice that the types for `Count` and `privateCount` are aligned. `go fmt` does that too, though unaligned fields are legal Go.

## Unused variables and imports

1. Unused variables and imported packages are illegal in Go. `go fmt` will remove them.

## Editor Integration

1. You can use `go fmt` on the command line yourself
    ```sh
    $ go fmt foo.go
    ```
1. Most editors with specialized Go support call `go fmt` when you save a source file.
1. VS Code has nice integration with Go. I hear that [vim-go](https://github.com/fatih/vim-go) is helpful, but don't use that myself.
1. I like the [micro](https://micro-editor.github.io/) terminal editor, so I wrote some [small improvements](https://github.com/phpeterson-usf/micro/commit/5c1651ff094db1672beaeefca5a0e9044b18a62e) to `go run` and `go fmt` on save.
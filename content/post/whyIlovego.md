---
author: "Kaarthik"
date: 2017-12-26
linktitle: Why I love Go
title: My relationship with Go
weight: 10
tags: ["go", "golang","technology"]
categories : ["technology"]
---
I have a love-hate relationship (more love and less hate :P) with any new programming language I pick up. This post describes my relationship with Go.

## Why I love it
---

I was introduced to <a href="https://golang.org/" target="_blank">Go</a> by <a href="https://typemismatch.org/" target="_blank">Bjoern</a> as a part of my student job and I have been smitten by it ever since. Here are a few reason's why I love go, in no particular order :

### Fast Compilation

Most popular languages are atleast a decade old and do not take advantage of the newer hardware. But, Go on the other hand is designed to run on modern computers and takes advantages of the faster hardware. This is partly the reason why Go compiles code like hot knife through butter. Another reason for the blazing fast build times is the way Go compiler performs <a href="https://en.wikipedia.org/wiki/Dependence_analysis" target="_blank">Dependency Analysis </a>. Below are a few points which I ripped from the <a href="https://golang.org/doc/faq" target="_blank">Go FAQs</a> page which summarizes why Go compiles code like there is no tomorrow:). If you are a Go developer and haven't gone through the FAQs, shame on you :P.

> Dependency management is a big part of software development today but the “header files” of languages in the C tradition are antithetical to clean dependency analysis—and fast compilation.

> Go provides a model for software construction that makes dependency analysis easy and avoids much of the overhead of C-style include files and libraries.

> Go's type system has no hierarchy, so no time is spent defining the relationships between types. Also, although Go has static types the language attempts to make types feel lighter weight than in typical OO languages.

### Static Compilation

Go compiles everything statically and produces a single binary. The end user of the executable can "simply" run the executable without worrying about installing the runtime or additional libraries.   

### Syntax

Of all the languages I have used, Go has the cleanest and easiest syntax. Here are a few things I like about the Go syntax :

**No semicolon** - Semicolon is a thing of the past. With Go there is no need to end every line of code with a semicolon.

 **Short variable declarations** - This one's my favourite. The ":=" operator is basically a short hand for variable declaration and assignment. Keep in mind that this shorthand can be used only inside functions.

```go
package main

import "fmt"

func main() {
	result := "best"
	fmt.Printf("Go is the %s",result)
}

```
**Multiple Return Values** - Go supports returning multiple values from a function. Most library functions return a result and an error. This is especially useful since Go has no built-in exceptions and exception handling mechanism. Instead Go uses the error type to indicate an abnormal state.

```go
package main
import "fmt"

//Returns multiple values
func getWords() (string, string) {
    return "hello", "world"
}
func main() {
    a, b := getWords()
    fmt.Printf("%s %s\n",a,b)
    //Ignore one of the returned values
    _, c := getWords()
    fmt.Println(c)
}
```

### OOP

Go is not completely object oriented. It has a type system, supports encapsulation and member functions but lacks inheritance. Go favours <a href="https://en.wikipedia.org/wiki/Composition_over_inheritance" target="_blank">"Composition over Inheritance"</a>. To understand more about OOP in Go please read this <a href="http://spf13.com/post/is-go-object-oriented/" target="_blank"> excellent blog post </a> by the great <a href="https://stevefrancia.com/" target="_blank">Steve Francia </a>. He goes into great detail about the advantages of the design decisions underlying Go's take on OOP.

### Concurrency

STOP! Before you read any further I suggest that you first watch this video by Rob Pike - <a href="https://www.youtube.com/watch?v=oV9rvDllKEg" target="_blank"> Concurrency is not Parallelism</a>. Go was designed with concurrency in mind. Go supports concurrency with Goroutines and Channels. Goroutines are lightweight threads which are managed by the runtime. Multiple goroutines are multiplexed on a single OS thread. This has multiple adavantages such as lesser memory consumption (approximately 2kb on the stack), lesser setup and teardown costs and lesser context switching costs. And spinning a goroutine is as easy as prefixing go to your function call as shown below.

```go
go getWords()
``` 

A channel is a data structure that is used to communicate between multiple goroutines. Traditionally threads in languages such as Java communicate with each other via Shared Memory which require you to acquire and release locks. But go follows a a different philosophy i.e. "Don't communicate by sharing memory, share memory by communicating". Goroutines communicate with each other by passing channels rather than acquiring locks to read and write from shared memory.

Heck! Go even has an built-in <a href="https://blog.golang.org/race-detector" target="_blank">race condition detector</a>.


### defer

I love defer(s) in Go. This <a href="https://blog.golang.org/defer-panic-and-recover" target="_blank">blog post</a> explains about defer.

> A defer statement defers the execution of a function until the surrounding function returns.


### Go tool

The go tool is the single most useful tool for managing Go source code. It does everything from formatting your source code to fetching all the dependencies. Here is a list of few of its capabilities:

1. build - compile packages and dependencies
2. clean - remove object files
3. doc - show documentation for package or symbol
4. fmt - run gofmt on package sources
5. get - download and install packages and dependencies
6. install - compile and install packages and dependencies
7. list - list packages
8. run - compile and run Go program
9. test - test packages


### Standard library

Go has a vast and exhaustive <a href="https://golang.org/pkg/" target="_blank">standard library</a> which includes everything from http server to logging. 

### Popularity

Go is here to stay. Firstly it is backed by Google and many of their products are written in Go. Other big organizations such as Adobe, SoundCloud, RyanAir etc use Go. (More exhaustive list <a href="https://github.com/golang/go/wiki/GoUsers" target="_blank">here</a>). This reinforces my faith and love for Go.

### The Community

The Go community is filled with wonderful and helpful people who are always ready to guide you in the right direction.

### This Blog :)


This website was created using a super-fast static site generator called <a href="https://gohugo.io/" target="_blank">Hugo</a> which is completely written in Go.

## Why I hate it
---

Here are a few reasons why I hate Go:

### Syntax

I just raved about how Go has a clean syntax, but here are a few rants :

1. Anything that starts with a uppercase is exported i.e. it is accessible from outside a package. Names starting with a lowercase are not exported.

2. No built-in enum support. As a developer with some background in C# I miss enums. (By using <a href="https://golang.org/ref/spec#Iota" target="_blank">iota</a> you can achieve enum-like functionality in Go)

3. I don't quite like the function signatures in Go.

> func funtionName(param1, param2..)(returnType1, returnType2..)

### Error Handling

I found the Error Handling in Go to be repetitive. If a function returns a result and an error, you are expected to check if the error is nil and then continue with you regular logic. And if the called function can return mutliple types of errors, then you would have to check for the type of the error in addition to checking if it is not nil. 

```go
info, err := echoReq.GetSlotValue(screenMessage)
if err != nil {
    // Do error handling
}else{
    // regular logic
}
```

### No Overloading and Optional Parameters

Yet again coming from C#, I miss method overloading and optional parameters which in my opinion are quite useful.

### The "else" problem

This is just me being picky and dumb, but coming from C# I have the habbit of writing the else condition in a new line rather than in the same line as the closing brace of the if condition. This results in a syntax error which makes me sad :(. <a href="https://play.golang.org/p/1NWNCItGU7s" target="_blank">Test it yourself.</a> 

```go
package main

import (
	"fmt"
)

func main() {
	a:=1
	if(a==1){
	    fmt.Println("a is one")
    }
    //This results in syntax error.
	else{
	    fmt.Println("a is not one")
	}
}
```

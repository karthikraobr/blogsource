---
author: "Kaarthik"
date: 2017-12-26
linktitle: Why I hate Go
title: Why I hate Go
weight: 10
tags: ["go", "golang",tech]
---
Here are a few reasons why I hate Go:

### Syntax
---
In my previous post I raved about how Go has a clean syntax, but here are a few reaons why I hate it :

1. Anything that starts with a uppercase is exported i.e. it is accessible from outside a package. Names starting with a lowercase are not exported.

2. No built-in enum support. As a developer with some background in C# I miss enums. (By using <a href="https://golang.org/ref/spec#Iota" target="_blank">iota</a> you can achieve enum-like functionality in Go)

3. I don't quite like the function signatures in Go.

> func funtionName(param1, param2..)(returnType1, returnType2..)

### Error Handling
---
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
---
Yet again coming from C#, I miss method overloading and optional parameters which in my opinion are quite useful.

### The "else" problem
---
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
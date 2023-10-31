---
title: "How to get a float number as an input using bufio in golang"
description: "In Golang, the `bufio` package provides a convenient way to handle input from various sources, including the standard input. While `bufio` is commonly used for reading strings and bytes, there are cases when you might want to read a floating-point number as input. In this article, we'll explore how to achieve this using a degree to radian converter example."
image: "images/post/golang-bufio-with-float-input.png"
date: 2023-03-12T18:19:25+06:00
categories: ["programming"]
tags: ["bufio", "coding", "golang"]
type: "reguler" # available types: [featured/regular]
draft: false
sitemapExclude: false
---

In Golang, the `bufio` package provides a convenient way to handle input from various sources, including the standard input. While `bufio` is commonly used for reading strings and bytes, there are cases when you might want to read a floating-point number as input, although it may be a bit complex, it isn't difficult to achieve. In this article, we'll explore how to achieve this 

### Introduction
First, let's grasp the essence of the bufio package. This package provides buffered I/O operations that enhance the efficiency of input and output operations in Golang. It allows for efficient reading and writing of data by minimizing the number of system calls, thus optimizing performance.

<br>

#### Reading Strings and Bytes:
When dealing with input, reading strings and bytes is straightforward using the bufio package. It's as simple as importing the package and using the ReadString or ReadByte function

<br>

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
package main
import (
    "fmt"
    "bufio"
)
func main() {
    reader := bufio.NewReader(os.Stdin)
    strInput, err := reader.ReadString('\n')
        if err != nil {
            fmt.Println( err)
        }
}
{{< / highlight >}}

<br>

However, handling floating-point numbers requires a slightly different approach, there are no inbuilt function in bufio to ReadFloat, and we can't use the ReadByte function because there will be some inaccuracys. 

#### Reading Floating-Point Numbers:
I'll try to keep the explanation short and get to the point, but if you want a more detailed explanation, I used two simple examples to explain it here at `Building a radian to Degree golang converter`, `Building a golang CLI job application`.

Let's get started:

<br>

1. Prompt the user to enter an input
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
fmt.Println("Enter a number")
{{< / highlight >}}

2. Read the input as a string using `bufio`.
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
reader := bufio.NewReader(os.Stdin)
strInput, err := reader.ReadString('\n')
	if err != nil {
		fmt.Println( err)
	}
{{< / highlight >}}

3. Readstring function parses a newline widespace `\n\r` to the end of our string which means every input we get will be attached to a widespace `\n\r`, this will prove troublesome when we try to get our desired value, so we have to get rid of it, here's a solution I came up with:

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
remSpc := strInput[:len(strInput)-2]
{{< / highlight >}}

This removes the two chars at the end of a string.

Although a much cleaner way to do this would be to use the TrimSpace function that comes with the `stings package`
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
remSpc := strings.TrimSpace(strInput)
{{< / highlight >}}

`Read this to understand better on how this works and other ways to carry it out.`

4. Convert the input string to a floating-point number using the `strconv` package.
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
ourFloat, err := strconv.ParseFloat(remSpc, 64)
	if err != nil {
		fmt.Println( err)
	} else {
        fmt.Printf("You entered %f :", ourFloat)
    }
{{< / highlight >}}

<br>

That's it. We're done. Your code should look like this:

<br>

{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
package main
import (
    "fmt"
    "bufio"
    "os"
    "strconv"
)

func main()  {
fmt.Println("Enter a number")
reader := bufio.NewReader(os.Stdin)
strInput, err := reader.ReadString('\n')
	if err != nil {
		fmt.Println( err)
	}
remSpc := strInput[:len(strInput)-2]
ourFloat, err := strconv.ParseFloat(remSpc, 64)
	if err != nil {
		fmt.Println( err)
	} else {
        fmt.Printf("You entered %f :", ourFloat)
    }
}
{{< / highlight >}}

<br>

#### Conclusion
In essence, this article provides a comprehensive walkthrough of effectively handling floating-point input using the bufio package in Go.
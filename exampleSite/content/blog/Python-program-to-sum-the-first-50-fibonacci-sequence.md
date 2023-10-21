---
title: "Python program to sum the first 50 fibonacci sequence"
description: "Fibonacci sequence is a sequence in which each number is equal to the sum of the two preceding numbers.The sequence usually starts with 0 and 1 and the next number would be the sum of the last two numbers"
image: "images/post/post-11.png"
date: 2023-07-24T18:19:25+06:00
categories: ["Algorithms"]
tags: ["programming", "datastructures", "algorithms"]
type: "regular" # available types: [featured/regular]
draft: false
---

## What is Fibonacci sequence?

Fibonacci sequence is a sequence in which each number is equal to the sum of the two preceding numbers.The sequence usually starts with 0 and 1 and the next number would be the sum of the last two numbers, in this case here you can guess it would be 1 because 1+0 = 1, our sequence should now look like this: 
    {{< highlight html >}}
            0,1,1,
    {{< /highlight >}}
you can guess what our next number should be, 1+1=2, so now our sequence looks like this: 
{{< highlight html >}}
            0,1,1,2.... 
{{< /highlight >}}
Seems quite easy right?. The simple rule is each number is equal to the sum of the preceding two numbers. Here's a sequence of the first 15 Fibonacci numbers,
            {{< highlight html >}}
             0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377.
            {{< /highlight >}}


### Sum The First 50 Fibonacci Sequence in Python
Now we've gotten to understand how fibonacci sequence works, let's move on to writing our python program to calculate the sum of the first 50 fibonacci series


#### Pre-requisite
I'll assume you already have a basic understanding of how python works. All you need is python installed on your computer, a code editor, notepad or whatever you write code on you can join in on your notebook too, it's just a simple python program


#### Display Fibonacci Sequence Python
Before we go into calculating the sum of first 50 fibonacci numbers, let me explain a simple approach to generating fibonacci sequence.

We are already aware that the first two numbers are 0 and 1. All other numbers are obtained by adding the preceding two numbers. This means to say the nth term is the sum of (n-1)th and (n-2)th term.

Let's generate fibinacci sequence up to the 50th number

{{< highlight python "linenos=table,hl_lines=8 15-17,linenostart=22" >}}
# let's declare our first two numbers
n1, n2 = 0, 1
count = 0

#let n be our number of terms
n = 50

#create a while loop to generate the sequence
while count < n:
    print(n1)
    nth = n1 + n2
    # update values
    n1 = n2
    n2 = nth
    count += 1
{{< / highlight >}}


This is an easy way to generate fibonacci sequence in python. Now let's try a different approach for finding the sum of the 50 terms.

In this method we will be creating a list(or array) that will hold each term and then we will use the sum function to add all elements of the list(array)

{{< highlight python "linenos=table,hl_lines=8 15-17,linenostart=199" >}}
def fibonacci_sequence():
    # starting with our first two numbers 0 and 1.
    fib_sequence = [0, 1]           
    

    # while loop to generate Fibonacci numbers until the length 50
    while len(fib_sequence) < 50:
    # Calculating the next Fibonacci number by adding the 
    last two numbers in the sequence     
        next_num = fib_sequence[-1] + fib_sequence[-2]  

        #Add each newly generated fibonacci number to the end of
         our list using the Append keyword
        fib_sequence.append(next_num)
    
    fib_sum = sum(fib_sequence)
    return fib_sum


result = fibonacci_sequence()
print("The sum of the first 50 Fibonacci numbers are:", result)
{{< / highlight >}}


And there, you have it.  This should successfully output our sum which should be 20365011073. 


Hope you found this short tutorial helpful, leave a comment if you do and maybe check out our other content, you may find something you enjoy.



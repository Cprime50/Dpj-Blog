---
title: "Differences Between Keywords and Reserved words and why some Languages exempt Reserved words"
description: "Reserved words are identifiers that are off-limits for naming variables, functions, or labels, preventing ambiguity and maintaining a clear syntax. Keywords, on the other hand, are a subset of reserved words, holding predefined meanings and functionalities that guide specific actions in the code."
image: "images/post/reservedwords-and-keywords-fotran.png"
date: 2023-06-29T18:19:25+06:00
categories: ["programming"]
tags: ["bufio", "coding", "golang"]
type: "reguler" # available types: [featured/regular]
draft: true
sitemapExclude: false
---

"I love cooking my family and my dog." You're probably thinking I'm an obscure cannibal now; well, I don't blame you for that. Now read again, "I love cooking, my family, and my dog." It makes much more sense now. Both these sentences can be interpreted as different meanings with just a comma, just as you may have been uncertain about my statement, computers also can't handle this kind of uncertainty, so they need clear and direct statements.

### Introduction
In programming languages, reserved words (also called reserved identifiers) are like commas in our sentences - they play a crucial role in defining clear boundaries. They are special words that can't be used as names for variables, functions, or labels; they're "reserved from use." It's a syntax rule, and they may not have any custom meaning.
Similarly, we have keywords, which act as little guides to specific meanings in certain situations. Very often you see people use "reserved word" and "keyword" interchangeably, I am also a victim of this but after a bit of researching I have come to understand the difference between them.
Just like how the comma made all the difference in "cooking my family and my dog," reserved words and keywords are like gatekeepers of clarity in programming languages. They don't necessarily have to be the same, but in modern languages, keywords are usually a subset of reserved words.Take the example of C or Python, where reserved words and keywords are the same, working hand in hand. Then, in Java, all keywords are reserved words, but not all reserved words are keywords. And in older languages like ALGOL, FORTRAN, and PL/I, there are keywords, but no reserved words.


### Why are keywords called Keywords?

Keywords in a programming language are predefined words with specific meanings and functionalities. They are reserved words that developers cannot use as names for variables, constants, or functions within the language. These keywords are carefully selected by the language designers to represent fundamental operations, control structures, and other essential functionalities.

The reason for reserving these words is to avoid ambiguity and ensure that the language's syntax remains unambiguous and well-defined. When a developer uses a keyword as the name of a variable, constant, or function, it may lead to confusion during compilation because the compiler expects that keyword to be used in a specific context. This can result in errors or unexpected behavior in the program.

To prevent clashes with reserved words, you must follow the language's syntax rules and use appropriate names for variables, constants, and functions to create clear and maintainable code that is easily understood by both humans and the compiler.

Keywords serve a number of common objectives. By letting programmers to use words rather than having to spell out every command, they enable them to write code more quickly.
It would be far simpler to merely type "print Hello World" and tell the computer what each word means rather than, for instance, typing out each letter separately if you wanted your programme to print "Hello World" on the screen. "Print" is a keyword in this example since it instructs the computer exactly what should happen when that line of code runs. Other keywords include FOR/NEXT (which tells the computer how many times something has to repeat) and IF/ELSE/ENDIF (which instructs the computer how to handle specific conditions).
There are certain words in every programming language that are forbidden from being used as variable names. Sometimes, reserved names are used to refer to keywords.


### Why do Fotran use keywords instead of reserved words?

Fortran has a long history and has gone through multiple revisions and standards. The decision not to reserve keywords as reserved words in Fortran is likely a result of various factors that have evolved over time. Here are some reasons why Fortran have chosen to reserve all keywords as reserved words:

1. Backward Compatibility: Fortran is a widely used and mature language with a significant amount of legacy codebases. Reserving all keywords as reserved words could break existing code that uses these keywords as identifiers. To maintain backward compatibility and avoid breaking existing code, Fortran developers might have chosen to follow a more cautious approach.

2. Flexibility and Usability: Fortran aims to be a versatile language, allowing developers to write code in various styles and with different coding practices. Allowing some keywords to be used as identifiers provides greater flexibility to programmers. For example, using "value" as a variable name might make the code more readable and understandable in certain contexts.

3. Balance Between Usability and Safety: Striking a balance between usability and safety is crucial in language design. By not reserving all keywords, Fortran allows programmers to use certain keywords as identifiers, making the language less restrictive. However, it also requires developers to be careful when using these keywords to avoid potential conflicts.

4. Compiler Warnings: As you mentioned, compilers can warn against using keywords as identifiers. This provides developers with information about potential issues and allows them to make informed decisions about naming variables and identifiers.

5. Historical Development: Fortran has evolved over several decades, and decisions about keyword reservation might have been made at different points in its history. The design choices reflect the language's development and the prevailing programming practices at the time.

In summary, the decision not to reserve all keywords as reserved words in Fortran is likely a result of balancing backward compatibility, language flexibility, and the desire to avoid breaking existing codebases. While it can lead to potential issues if keywords are used as identifiers, compilers can provide warnings to help programmers avoid these pitfalls. Language design is a complex process that involves trade-offs, and each programming language usually strike a balance that meets the needs of its users and community.


### Summary:
Reserved words and keywords are foundational elements in programming languages, with unique roles that contribute to code structure and readability. Reserved words are identifiers that are off-limits for naming variables, functions, or labels, preventing ambiguity and maintaining a clear syntax. Keywords, on the other hand, are a subset of reserved words, holding predefined meanings and functionalities that guide specific actions in the code. While these terms are sometimes used interchangeably, they have nuanced differences that impact programming practices.

By examining the rationale behind these language features, we gain insight into their importance. Reserved words and keywords serve as gatekeepers of clarity, ensuring that code remains unambiguous and predictable. While some languages, like C and Python, merge the two concepts, others, such as Fotran, differentiate between them. Ultimately, understanding the interplay between reserved words and keywords can help developers to craft code that is both comprehensible and effective in conveying computational instructions.
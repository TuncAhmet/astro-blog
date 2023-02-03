---
title: String Functions
description: Learn about string functions in C programming language.
date: 2021-05-31
category: C
---

# String Functions

You need to often manipulate [strings](https://www.programiz.com/c-programming/c-strings) according to the need of a problem. Most, if not all, of the time string manipulation can be done manually but, this makes programming complex and large.

To solve this, C supports a large number of string handling functions in the [standard library](https://www.programiz.com/c-programming/library-function) `"string.h"`.

Few commonly used string handling functions are discussed below:

| Function                                                        | Work of Function                |
| --------------------------------------------------------------- | ------------------------------- |
| https://www.programiz.com/c-programming/library-function/strlen | computes string's length        |
| https://www.programiz.com/c-programming/library-function/strcpy | copies a string to another      |
| https://www.programiz.com/c-programming/library-function/strcat | concatenates(joins) two strings |
| https://www.programiz.com/c-programming/library-function/strcmp | compares two strings            |
| strlwr()                                                        | converts string to lowercase    |
| strupr()                                                        | converts string to uppercase    |

### \***\*gets() and puts()\*\***

Functions gets() and puts() are two string functions to take string input from the user and display it respectively as mentioned in the [previous chapter](https://www.programiz.com/c-programming/c-strings).

```c
#include<stdio.h>

int main()
{
    char name[30];
    printf("Enter name: ");
    gets(name);     //Function to read string from user.
    printf("Name: ");
    puts(name);    //Function to display string.
    return 0;
}
```

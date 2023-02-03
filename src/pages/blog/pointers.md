---
title: Pointers
description: Pointers are a very important concept in C programming. In this article, we will learn about pointers in C programming with examples.
date: 2021-05-31
category: C
---

# Pointers

## Introduction to Pointers

### \***\*Assigning addresses to Pointers\*\***

Let's take an example.

```c
int* pc, c;
c = 5;
pc = &c;
```

Here, 5 is assigned to the c variable. And, the address of c is assigned to the pc pointer.

### \***\*Get Value of Thing Pointed by Pointers\*\***

To get the value of the thing pointed by the pointers, we use the `*` operator. For example:

```c
int* pc, c;
c = 5;
pc = &c;
printf("%d", *pc);   // Output: 5
```

Here, the address of `c`
 is assigned to the pc
 pointer. To get the value stored in that address, we used \*pc
.

<aside>
💡 **Note:** In the above example, pc is a pointer, not `*pc`. You cannot and should not do something like `*pc = &c`;

By the way, `*` is called the dereference operator (when working with pointers). It operates on a pointer and gives the value stored in that pointer.

</aside>

### \***\*Common mistakes when working with pointers\*\***

Suppose, you want pointer pc to point to the address of c. Then,

```c
int c, *pc;

// pc is address but c is not
pc = c;  // Error

// &c is address but *pc is not
*pc = &c;  // Error

// both &c and pc are addresses
pc = &c;  // Not an error

// both c and *pc are values
*pc = c;  // Not an error
```

## Pointers & Arrays

### **Relationship Between Arrays and Pointers**

An array is a block of sequential data. Let's write a program to print addresses of array elements.

```c
#include <stdio.h>
int main() {
   int x[4];
   int i;

   for(i = 0; i < 4; ++i) {
      printf("&x[%d] = %p\n", i, &x[i]);
   }

   printf("Address of array x: %p", x);

   return 0;
}
```

Output

```c
&x[0] = 1450734448
&x[1] = 1450734452
&x[2] = 1450734456
&x[3] = 1450734460
Address of array x: 1450734448
```

<aside>
💡 Notice that, the address of &x[0] and x is the same. It's because the variable name x points to the first element of the array.

</aside>

## Pointers & Functions

### **Example: Pass Addresses to Functions**

```c
#include <stdio.h>
void swap(int *n1, int *n2);

int main()
{
    int num1 = 5, num2 = 10;

    // address of num1 and num2 is passed
    swap( &num1, &num2);

    printf("num1 = %d\n", num1); // 10
    printf("num2 = %d", num2); // 5
    return 0;
}

void swap(int* n1, int* n2)
{
    int temp;
    temp = *n1;
    *n1 = *n2;
    *n2 = temp;
}
```

When *n1 and *n2 are changed inside the `swap()` function, num1 and num2 inside the main() function are also changed.

Inside the `swap()` function, `*n1` and `*n2` swapped. Hence, num1 and num2 are also swapped.

Notice that `swap()` is not returning anything; its return type is `void`.

## **Example 2: Passing Pointers to Functions**

```c
#include <stdio.h>

void addOne(int* ptr) {
  (*ptr)++; // adding 1 to *ptr
}

int main()
{
  int* p, i = 10;
  p = &i;
  addOne(p);

  printf("%d", *p); // 11
  return 0;
}
```

Here, the value stored at p, `*p`, is 10 initially.

We then passed the pointer p to the `addOne()` function. The ptr pointer gets this address in the `addOne()` function.

Inside the function, we increased the value stored at ptr by 1 using `(*ptr)++;`. Since ptr and p pointers both have the same address, `*p` inside `main()` is also 11.

## **C Dynamic Memory Allocation**

As you know, an array is a collection of a fixed number of values. Once the size of an array is declared, you cannot change it.

Sometimes the size of the array you declared may be insufficient. To solve this issue, you can allocate memory manually during run-time. This is known as dynamic memory allocation in C programming.

To allocate memory dynamically, library functions are `malloc()`, `calloc()`, `realloc()` and `free()` are used. These functions are defined in the `<stdlib.h>` header file.

### C Malloc()

The name "malloc" stands for memory allocation.

The `malloc()` function reserves a block of memory of the specified number of bytes. And, it returns a [pointer](https://www.programiz.com/c-programming/c-pointers) of `void` which can be casted into pointers of any form.

\***\*Syntax of malloc()\*\***

```c
ptr = (castType*) malloc(size);
```

example

```c
ptr = (float*) malloc(100 * sizeof(float));
```

The above statement allocates 400 bytes of memory. It's because the size of `float` is 4 bytes. And, the pointer ptr holds the address of the first byte in the allocated memory.

The expression results in a `NULL` pointer if the memory cannot be allocated.

### **C calloc()**

The name "calloc" stands for contiguous allocation.

The `malloc()` function allocates memory and leaves the memory uninitialized, whereas the `calloc()` function allocates memory and initializes all bits to zero.

\***\*Syntax of calloc()\*\***

```c
ptr = (castType*)calloc(n, size);
```

example

```c
ptr = (float*) calloc(25, sizeof(float));
```

The above statement allocates contiguous space in memory for 25 elements of type `float`.

### **C free()**

Dynamically allocated memory created with either `calloc()` or `malloc()` doesn't get freed on their own. You must explicitly use `free()` to release the space.

\***\*Syntax of free()\*\***

```c
free(ptr);
```

This statement frees the space allocated in the memory pointed by `ptr`.

\***\*Example 1: malloc() and free()\*\***

```c
// Program to calculate the sum of n numbers entered by the user

#include <stdio.h>
#include <stdlib.h>

int main() {
  int n, i, *ptr, sum = 0;

  printf("Enter number of elements: ");
  scanf("%d", &n);

  ptr = (int*) malloc(n * sizeof(int));

  // if memory cannot be allocated
  if(ptr == NULL) {
    printf("Error! memory not allocated.");
    exit(0);
  }

  printf("Enter elements: ");
  for(i = 0; i < n; ++i) {
    scanf("%d", ptr + i);
    sum += *(ptr + i);
  }

  printf("Sum = %d", sum);

  // deallocating the memory
  free(ptr);

  return 0;
}
```

\***\*Example 2: calloc() and free()\*\***

```c
// Program to calculate the sum of n numbers entered by the user

#include <stdio.h>
#include <stdlib.h>

int main() {
  int n, i, *ptr, sum = 0;
  printf("Enter number of elements: ");
  scanf("%d", &n);

  ptr = (int*) calloc(n, sizeof(int));
  if(ptr == NULL) {
    printf("Error! memory not allocated.");
    exit(0);
  }

  printf("Enter elements: ");
  for(i = 0; i < n; ++i) {
    scanf("%d", ptr + i);
    sum += *(ptr + i);
  }

  printf("Sum = %d", sum);
  free(ptr);
  return 0;
}
```

### **C realloc()**

If the dynamically allocated memory is insufficient or more than required, you can change the size of previously allocated memory using the `realloc()`
 function.

\***\*Syntax of realloc()\*\***

```c
ptr = realloc(ptr,x);
```

Here, ptr is reallocated with a new size x.

\***\*Example 3: realloc()\*\***

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  int *ptr, i , n1, n2;
  printf("Enter size: ");
  scanf("%d", &n1);

  ptr = (int*) malloc(n1 * sizeof(int));

  printf("Addresses of previously allocated memory:\n");
  for(i = 0; i < n1; ++i)
    printf("%pc\n",ptr + i);

  printf("\nEnter the new size: ");
  scanf("%d", &n2);

  // rellocating the memory
  ptr = realloc(ptr, n2 * sizeof(int));

  printf("Addresses of newly allocated memory:\n");
  for(i = 0; i < n2; ++i)
    printf("%pc\n", ptr + i);

  free(ptr);

  return 0;
}
```

<!-- markdownlint-disable MD001 -->

# C

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Error handling](#error-handling)
- [Dynamic memory allocation](#dynamic-memory-allocation)
- [Preprocessors](#preprocessors)
- [Macros](#macros)
- [Header files](#header-files)

### Print

```c
printf("Hello World! \n");
```

### Variables

```c
int x; /* declare */
x = 4; /* initialize */
int x = 4; /* declare and initialize */
const x = 4;
int *x; /* declare pointer variable */
auto int x; /* Default storage class for local variables */
register int x; /* Store variable in register instead of RAM */
static int x; /* Keep variable during lifetime of the program */
extern int x; /* Reference of a global variable visible to all program files */
```

### Data types

```c
/* Basic types */
int x;
float x;
double x;
char x;
char my_string[]; /* String as array of chars */

/* Boolean */
#include <stdbool.h>
bool x;

/* Array */
int arr[5] = {1, 2, 3, 4, 5};
int first_arr = arr[0];

/* Enum */
enum Color {Red, Green, Blue};

/* Struct */
struct User {
    char username[50];
    char email[50];
};

/* Declare and intialize struct */
struct User user;
strcpy(user.username, "someusername");
strcpy(user.email, "someone@example.com");

/* Union: store different data types in the same memory location */
union Data {
    int i;
    float f;
    char str[10];
}

/* Typedef: alias for a type */
typedef unsigned char BYTE;

/* Define: alias for values */
#define ONE 1

/* Type casting */
double x = 4.
x_converted = (int) x
```

### Control flow

```c
/* for loop */
for (a = 10; a < 20; a++) {
    /* statement */
}

/* while loop */
while(i < 3) {
    /* statement */
}

/* if-else */
if (a < b) {
    /* statement */
} else if (a == b) {
    /* statement */
} else {
    /* statement */
}

/* ? operator */
exp1 ? exp2 : exp3;

/* switch */
switch(x) {
    case 'A':
        /* statement */
        break;
    case 'B':
        /* statement */
        break;
    default:
        /* statement */
        break;
}
```

### Functions

```c
int my_function(int x) {
    int y = 3;
    return x + y;
}

void swap(int *x, int *y) {
    int temp;
    temp = *x;
    *x = *y;
    *y = temp;
    return;
}

/* call by value */
my_function(a)

/* call by pointer */
swap(&a, &b)

/* Variable number of parameters */
int my_function(int num, ... ) {
    /* statement */
}

/* Recursive function */
unsigned long long int factorial(unsigned int i) {
   if (i <= 1) {
      return 1;
   }
   return i * factorial(i - 1);
}
```

### Error handling

```c
/* Opening file */
#include <stdio.h>
#include <errno.h>
#include <string.h>

extern int errno;
FILE * pf;
pf = fopen ("unexist.txt", "rb");

if (pf == NULL) {
    fprintf(stderr, "Value of errno: %d\n", errno);
    perror("Error opening file");
}


/* Division by zero */
#include <stdio.h>
#include <stdlib.h>

if (divisor == 0) {
   fprintf(stderr, "Division by zero! Exiting...\n");
   exit(-1);
}
```

### Dynamic memory allocation

```c
char *ptr
ptr = malloc(100 * sizeof(char)); /* Allocate memory */
ptr = realloc(ptr, 500 * sizeof(char)); /* Resize allocated memory */
free(ptr); /* Release allocated memory */
```

### Preprocessors

```c
#define /* Substitutes a preprocessor macro */
#include /* Inserts a particular header from another file */
#undef /* Undefines a preprocessor macro */
#error
#pragma
```

### Macros

```c
/* Parameterized macro */
#define square(x) ((x) * (x))

/* Predefined macros */
__DATE__
__TIME__
__FILE__
__LINE__
```

### Header files

```c
/* System header files */
#include <header.h>

/* Program header files */
#include "my_header.h"
```

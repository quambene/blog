<!-- markdownlint-disable MD001 -->

# Typescript

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Error handling](#error-handling)

### Print

```javascript
console.log('Hello world');
console.table({foo, bar});
console.group();
console.groupEnd();
console.warn();
console.error();
console.time();
```

### Variables

```javascript
let x: number = 4;
const x: number = 2;
let x = `Hello ${firstName} ${lastName}`; // template string
let x = (condition) ? valueIfTrue:valueIfFalse; // conditional operator
let x = myEntity!.name; // non-null assertion operator
```

### Data types

```javascript
// Basic types
let x: number;
let x: string;
let x: boolean;
let x: any;
let x: void;
let x: null;
let x: undefined;

// Array
let arr: number[] = [1, 2, 3];
let arr: Array<number> = [1, 2, 3];
let first_arr = arr[0];

// Tuple
let tup: [string, number] = ['hello', 4];

// Enum
enum Color { Red, Green, Blue };
let green: Color = Color.Green;
```

### Control flow

```javascript
// while loop
while (i < 3) {
    // statement
 }

// if-else
if (a < b) {
    // statement
} else if (a == b) {
    // statement
} else {
    // statement
}

// switch
switch (variable_expression) {
    case constant_expr1: {
        //statement
        break;
    }
    case constant_expr2: {
        //statement
        break;
    }
    default: {
        //statement
        break;
    }
}
```

### Functions

```javascript
function myFunction(arg: number): number {
    return arg;
}

// Fat arrow function
let evens = [2, 4, 6, 8];
let odds = evens.map(v => v + 1);
```

### Classes

```javascript
class Person {
    first_name: string;
    last_name: string;

    constructor() {}

    greet(): void {
        console.log('Hello', this.first_name);
    }
}

// Instantiation
let person = new Person();
```

### Error handling

```javascript
try {
    // code to try
}
catch (err) {
    // code to handle errors
    if (err instanceof Error) {

    } else {
        throw(err);
    }
}
finally {
   // code to be executed regardless of the try-catch result
}
```

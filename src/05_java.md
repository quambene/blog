<!-- markdownlint-disable MD001 -->

# Java

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Error handling](#error-handling)
- [Interfaces](#interfaces)
- [Generics](#generics)

### Print

```java
System.out.println("Hello World");
```

### Variables

```java
int x; // declare
x = 4; // assign value
int x = 4;
String name = "John";
```

### Data types

```java
// Basic types
byte x;
short x;
int x;
long x;
float x;
double x;
boolean x;
char x;
String x;

// Array
int[] arr = {1, 2, 3};
first_arr[0];
int[][] arr2D = { {1, 2, 3}, {5, 6, 7, 8} };
first_arr2D = arr2D[0][0]

// Vector
ArrayList<String> arr_list = new ArrayList<String>();
arr_list.add("value1");
arr_list.get(0);

// Enum
enum Color {
    RED,
    GREEN,
    BLUE
}

// Hash map
HashMap<String, String> hashmap = new HashMap<String, String>();
hashmap.put("key1", "value1");
hashmap.get("key1");
hashmap.remove("key1");
```

### Control flow

```java
// for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// while loop
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}

// if-else
if (a < b) {
    // statement
} else if (a == b) {
    // statement
} else {
    // statement
}
```

### Functions

```java
// Method
public static int myMethod(int x) {
    return 5 + x;
}
```

### Classes

```java
public class MyClass {
    int x = 5; // class attribute
    final double PI = 3.14; // cannot be modified
    private String name; // restricted access (encapsulation)

    // class constructor
    public MyClass() {
        // ...
    }

    // static method
    static void myStaticMethod() {
        // ...
    }

    // public method
    public void myPublicMethod() {
        // ...
    }

    // main method
    public static void main(String[] args) {
        // ...
    }
}

// Instantiation
MyClass myObject = new MyClass();
myObject.x;
myObject.myPublicMethod(); // Call method
MyClass.myStaticMethod(); // Call static method

// Inheritance
class Vehicle {
    // ...
}

class Car extends Vehicle {
    // ...
}

// Polymorphism (method overriding)
class Vehicle {
    public void myMethod() {
        // ...
    }
}

class Car extends Vehicle {
    public void myMethod() {
        // ...
    }
}

// Abstract class (must be inherited from another class)
abstract class MyAbstractClass {
    // ...
}
```

### Interfaces

```java
// Group related methods
interface MyInterface {
    public void method1();
    public void method2();
}

// Implement interface
class MyClass implements MyInterface {
    public void method1() {
        // ...
    }

    public void method2() {
        // ...
    }
}
```

### Generics

```java
// Generic method
public static <T> void myGenericMethod(T[] myArray) {
    // ...
}

// Bounded type parameter
public static <T extends Comparable<T>> void maximum(T x, T y, T z) {
    // ...
}

// Generic class
public class MyGenericClass<T> {
    // ...
}
```

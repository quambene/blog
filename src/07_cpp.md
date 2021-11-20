<!-- markdownlint-disable MD001 -->

# C++

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

### Print

```cpp
#include <iostream>
cout << "Hello World";
```

### Variables

```cpp
int *x; // pointer

int y = 4;
int& ref = y; // reference (must be initialized)
```

### Data types

```cpp
bool x;

// String
#include <string>
string x;

```

### Functions

```cpp
void swap(int &x, int &y) {
    int temp;
    temp = x;
    x = y;
    y = temp;
    return;
}

/* call by reference */
swap(a, b)
```

### Classes

```cpp
class MyClass {
    public:
        MyClass() { // Constructor
            // statement
        };
        double x;
        double myMemberFunction() {
            // statement
        };

    private:
        double y;

    // can be accessed in child classes
    protected:
        double z;
}

// Instantiation
MyClass myclass;

// Inheritance
class MyDerivedClass: public MyBaseClass {
    // ...
}

// Function overloading
class MyClass {
    public:
        void myFunction(int i) {
            // ...
        }
        void myFunction(double f) {
            // ...
        }
        void myFunction(char c) {
            // ...
        }
}

// Polymorphism
class MyBaseClass {
    public:
        virtual int myFunction() {
            // ...
        }
}

class MyDerivedClass1: public MyBaseClass {
    public:
        int myFunction() {
            // ...
        }
}

class MyDerivedClass2: public MyBaseClass {
    public:
        int myFunction() {
            // ...
        }
}
```

### Interfaces

```cpp
class MyAbstractClass {
    public:
        // Pure virtual function
        virtual int myFunction() = 0;
}
```

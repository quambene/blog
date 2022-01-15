<!-- markdownlint-disable MD001 -->

# Dart

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Mixins](#mixins)
- [Generics](#generics)
- [Async](#async)
- [Concurrency](#concurrency)
- [Error handling](#error-handling)
- [Null safety](#null-safety)

### Print

```dart
var name = "world";
print('Hello $name');
print('Hello ${name}');
```

### Variables

```dart
var x = 'Smith';
String x = 'Bob'; // typed
final x = 42; // immutable
const x = 42; // immutable at compile-time
int x = optionalValue() ?? exprIfNull; // default operator
int x ??= 4; // fallback assignment operator
var x = condition ? exprIfTrue : exprIfFalse // conditional operator
```

### Data types

```dart
// Basic types
String x;
int x:
double x;
bool x;
Object? x; // referencing any object, including null
Object x; // referencing any object, excluding null
dynamic x; // disables static type-checking

// List
var myList = []; // initialize empty list
var myList = List(); // initialize empty list
var myList = List(5) // fixed length
var myList = [1, 2, 3] // growable length
myList[0] = 'value' // initialize
myList = [...myList1, ...myList2] // List comprehension

// Map
var myMap = Map(); // initialize empty map
var myMap = { 'key1': 'value1', 'key2': 'value2' };
Map<String, String> myMap = { 'key1': 'value1', 'key2': 'value2' }; // typed

// Enum
enum Color { Red, Green, Blue };
```

### Control flow

```dart
// for loop
for (var i = 0; i <= 3; i++) {
    print(i);
}

// for ... in loop
for (car in cars) {
    print(car);
}

// while loop
while (i <= 5) {
    print(i);
    i++;
}

// do ... while loop
do {
    print(i);
    i++;
}
while (i <= 5);

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
    }
    break;

    case constant_expr2: {
        //statement
    }
    break;

    default: {
        //statement
    }
    break;
}
```

### Functions

```dart
int my_function(int param, [int optional_param], {int default_param = 42} ) {
    return param;
}

// Lambda functions (fat arrow expression)
int my_lambda() => 42;

// Lexical scope
var name = 'peter';
var getUpperCase = () {
    name.toUpperCase();
}

// Closure
var addNumber = (num i) {
    return (num j) => i+j;
}
```

### Classes

```dart
class MyClass {
    static String name;
    final int myFinalVar1;
    final int myFinalVar2;
    int myProperty1;
    int myProperty2;
    int myPublicVariable;
    int _myPrivateVariable;

    // class constructor
    MyClass() {
        // ...
    }

    // parameterized constructor
    MyClass(String param1, String param2) {
        this.myProperty1 = param1;
        this.myProperty2 = param2;
    }

    // parameterized constructor (short form)
    MyClass(this.myProperty1, this.myProperty2);

    // named optional parameters
    MyClass({this.myProperty1, this.myProperty2});

    // named required parameters
    MyClass({required this.myProperty1, required this.myProperty2});

    // initializer list
    MyClass(String param1, String param2)
    : this.myFinalVar1 = param1,
      this.myFinalVar2 = param2;

    // named constructor
    MyClass.myConstructor(String param) {
        // ...
    }

    factory MyClass.myConstructor(String param) {
        return MyClass(
            //...
        );
    } 

    // static method
    static void myStaticMethod() {
        // ...
    }

    // public method
    public void myPublicMethod() {
        // ...
    }

    void set name(String name) {
        this.name = name;
    }

    String get name {
        return name;
    }
}

MyClass myObject = new MyClass(); // Create instance
myObject.myProperty; // Access attribute
myObject?.myProperty // Conditional access (if not null)
myObject.myPublicMethod(); // Call method
myObject?.myPublicMethod(); // Conditional access (if not null)
MyClass.myStaticMethod(); // Call static method
MyClass()..myMethod(); // Cascade notation

// Inheritance and method overriding
class ParentClass {
    void my_method() {
        // ...
    }
}

class ChildClass extends ParentClass {
    @override
    void my_method() {
        // ...
    }
}
```

### Interfaces

```dart
class MyInterface {
   void my_function() {}
}

class MyClass implements MyInterface {
   void my_function() {  
      // implementation
   }
}
```

### Mixins

```dart
mixin MyMixin {
   void my_function() {}
}

class MyClass with MyMixin {
    // ...
}

// Restrict types that can use a mixin
mixin MyMixin on MyClass {
    // ...
}
```

### Generics

```dart
// Generic class
class Property<T> {
    T first, second;
    Property(this.first, this.second);
}
```

### Async

```dart
Future<String> fut_str = file.readAsString();
fut_str.then((data) => print(data));

// async-await
Future<void> my_function() async {
    await my_async_function();
}
```

### Concurrency

```dart
Isolate.spawn(spawned_function1, message1);
Isolate.spawn(spawned_function2, message2);
```

### Error handling

```dart
try {
    // code that might throw an exception
}
on FormatException catch(err) {
    // handle FormatException
}
on Exception catch(err) {
    // handle other exceptions
}
catch (err) {
    // propagate error
    rethrow
}
```

### Null safety

``` dart
String myString;
String? myNullableString;

class MyClass {
    final String myProperty;
    late String name;

    MyClass(required this.myProperty)
}

myObject?.myName
myObject!.myName

class MyClass {
    String? myProperty;

    void myMethod() {
        // type promotion (to a non-nullable type)
        final myProperty = this.myProperty;
        
        if (myProperty != null) {
            //...
        }
    }
}
```

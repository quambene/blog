<!-- markdownlint-disable MD001 -->

# Go

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Error handling](#error-handling)
- [Concurrency](#concurrency)

### Print

```go
fmt.Println("Hello World")
fmt.Println("1+1 =", 1+1)
```

### Variables

```go
var x int // declared variables are zero-valued
var x int = 4 // declare and initialize
x := 4 // shorthand for declare and initialize
const s string = "constant"
var x *int // pointer
*x = 4 // dereference
&x // address of pointer
```

### Data types

```go
// Basic types
var x int
var x int64
var x float32
var x float64
var x string

// Array
arr := [3]int{1, 2, 3}

// Slice
my_slice := make([]int, 3)
my_slice = append(my_slice, 1)

// Map (hash map)
my_map := make(map[string]string)
my_map["key1"] = "value1"

// Struct
type user struct {
    username string
    email string
}

// Initialize struct
u := user{username: "Alice", email: "alice@example.com"}
u.username
```

### Control flow

```go
// for loop
for i := 1; i <= 3; i++ {
    fmt.Println(i)
}

// if-else
if a < b {
    // statement
} else if a == b {
    // statement
} else {
    // statement
}

// switch
i := 2
switch i {
case 1:
    // statement
case 2:
    // statement
case 3:
    // statement
default:
    // statement
}
```

### Functions

```go
func myFunction(a int, b int) (int, int) {
    return a, b
}

// Variadic function (any number of arguments)
func myFunction(nums ...int) {
    // ...
}

// Closure (lambda expression)
func myFunction() func() int {
    i := x
    return func() int {
        i++
        return i
    }
}

// Recursive function
func factorial(n int) int {
    if n == 0 {
        return 1
    }
    return n * factorial(n-1)
}

// Methods (on structs)
func (s myStruct) myFunction() {
    // ...
}
```

### Interfaces

```go
type myInterface interface {
    myMethod1() int
    myMethod2() int
}

// Implementation of interface
func (s myStruct) myMethod1 int {
    // ...
}

func (s myStruct) myMethod2 int {
    // ...
}

```

### Error handling

```go
func myFunction(arg int) (int, error) {
    if arg == 0 {
        return -1, errors.New("error message")
    }

    return arg, nil
}
```

### Concurrency

```go
// Goroutines: Run functions asynchronously
func main() {

    go myFunction1()

    go myFunction2()
}

// Channels: Synchronize goroutines
myChannel := make(chan string)
go func() { myChannel <- "ping" }() // Send value into channel
msg := <-myChannel // Receive value from channel
```

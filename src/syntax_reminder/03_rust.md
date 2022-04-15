<!-- markdownlint-disable MD001 -->

# Rust

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Generics](#generics-parametric-polymorphism)
- [Traits](#traits-ad-hoc-polymorphism)
- [Lifetimes](#lifetimes)
- [Macros](#macros)
- [Error handling](#error-handling)
- [Testing](#testing)
- [Modules](#modules)
- [Crates](#crates)
- [Packages](#packages)
- [External packages](#external-packages-cargo.toml)
- [Cargo](#cargo-package-manager)

### Print

```rust
let name = "world";
println!("Hello, {}!", name);
println!("Debug: {:?}", name); // for debugging
println!(":#?", my_struct); // pretty-print structs
```

### Variables

```rust
/*  Ownership rules:
    - each value in Rust has a variable that’s called its owner
    - there can only be one owner at a time
    - when the owner goes out of scope, the value will be dropped */

let x; // declare
x = 4; // assign value
let x = 4;
let x: i32 = 4; // assign value (typed)
let _x = 4; // compiler won't warn about variable being unused
let x = x + 1; // shadowing
let mut x; // mutable
let x: &i32; // reference: refer to some value without taking ownership of it
*x // dereferencing
let x: &'a i32; // reference with an explicit lifetime
let x: &'a mut i32; // mutable reference with an explicit lifetime
let x: *const i32; // const pointer
let x: *mut i32; // // mut pointer
const MYCONST: f32 = 3.14; // immutable value
static MYSTATIC: &str = "Rust"; // mutable variable with static lifetime
let r#fn = "name"; // raw identifier for reserved keywords
```

### Data types

```rust
// Basic types
let x: i32; // signed integer
let x: i64;
let x: u32; // unsigned integer
let x: u64;
let x: f32; // floating point
let x: f64;
let x: &str; // borrowed string slice
let x: String; // owned string type
let x: &'static str; // string with static lifetime
let x: bool;
let x: char = 'ℤ'; // unicode character
let x: &[T]; // slice
let x: &mut [T]; // mutable slice

// Type alias
type MyId = u32;
type Point = (u8, u8);

// Array
let arr: [i32; 5] = [1, 2, 3, 4, 5];
let first_arr = arr[0];

// Tuple
let tup: (i32, f64, u8) = (500, 6.4, 1);
let first_tup = tup.0; // access a tuple element
let (x, y, z ) = tup; // destructuring

// Vector
let vec: Vec<i32> = Vec::new();
let vec = vec![1, 2, 3];
let first_vec = vec.get(0);
let first_vec = &vec[0];
vec.push(4);

// Slice
// view into a vector, cannot grow
let s = &my_arr[1..3]
let s = &my_vec[1..3]

// Hash map
let mut my_hashmap = HashMap::new();
my_hashmap.insert(String::from("Key1"), String::from("Value1"));

// Enum
enum Option<T> {
    Some(T),
    None,
}

enum Result<T, E> {
    Ok(T),
    Err(E),
}

enum Color {
    Red,
    Green,
    Blue,
}

let red = Color::Red;

// Struct (custom data type)
struct MyStruct; // unit struct
struct MyStruct(i32, i32); // tuple struct
struct Email(String) // newtype pattern

struct User {
    username: String,
    email: String,
}

// Instantiation of struct
let user = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername"),
}

// Store references (see lifetimes)
struct User {
    username: &str,
    email: &str,
}

// Smart pointer (Heap allocation)
Box<T> // pointer type for heap allocation
Rc<T> // single-threaded reference-counting pointer (reference counted)
Arc<T> // thread-safe reference-counting pointer (atomically reference counted)
```

### Control flow

```rust
// for loop
for element in set {
    // statement
};

// while loop
while i < 3 {
    // statement
};

// if-else
if a < b {
    // statement
} else if a == b {
    // statement
} else {
    // statement
};

// pattern matching
match my_option {
    Some(i) => Some(i + 1),
    None => None,
}

match some_value {
    4 => println!("four"),
    _ => (),
}

// if let
if let Some(i) = my_option {
    println!("Matched {}", i)
} else {
    println!("Didn't match")
}

// while let
while let Some(i) = my_option  {
    println!("Matched {}", i)
}
```

### Functions

```rust
fn my_function(x: i32) -> i32 {
    let y = 3; // statement
    x + y // expression (return value without semicolon)
}

// Method (similar to classes in OOP)
impl MyStruct { // implement struct
    fn my_function(&self) -> i32 {
        // ...
    }
}
my_struct.my_function(); // call method

// Associated function
impl MyStruct {
    fn my_function(x: i32) -> i32 {
        // ...
    }
}
MyStruct::my_function(42); // call associated function

// Closure
let my_closure = |i| i + 1;
let my_closure = |i: i32| -> i32 { i + 1 }; // typed
```

### Generics (parametric polymorphism)

```rust
fn my_generic_function<T>(list: &[T]) -> T {
    // ...
}

impl<T> MyGenericStruct<T> {
    fn my_function(&self) -> &T {
        // ...
    }
}
```

### Traits (ad-hoc polymorphism)

```rust
// A collection of methods defined for an unknown type
trait MyTrait {
    fn new(name: &'static str) -> Self;
    fn my_method(&self) -> String;
    fn default_method(&self) {
        // ...
    };
}

impl MyTrait for String {
    fn my_method(&self) -> String { format!("string: {}", *self)
}

impl MyTrait for u8 {
    // ...
}

impl MyTrait for MyStruct {
    // ...
}

// static dispatch
fn do_something<T: MyTrait>(x: T) {
    x.my_method();
}

// dynamic dispatch
fn do_something(x: &MyTrait) { // trait object &MyTrait
    x.my_method();
}

impl dyn MyTrait {
    // ...
}

// trait bounds
struct MyStruct<T: MyTraitBound>(T);

fn my_function<T: MyTraitBound>(t: T) {}

fn my_function(t: impl MyTraitBound) {}

fn my_function<T, U>(t: &T, u: &U) 
where 
    T: Display + Clone,
    U: AsRef<str>,
{}

// Supertrait (a superset of another trait)
trait MyTrait: MySuperTrait {
    fn my_method(&self) -> String;
}
```

### Lifetimes

```rust
/*  Every reference has a lifetime;
    and lifetime parameters for functions or structs
    that use references have to be specified */
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

### Macros

```rust
use my_macro::MyMacro;
use my_macro_derive::MyMacro;

#[derive(MyMacro)]
struct MyStruct;

fn main() {
    MyStruct::my_macro();
}

// other macros
unimplemented!() // satisfies the type checker without providing an implementation
```

### Error handling

```rust
// ? operator (propagating errors)
fn read_username_from_file() -> Result<String, io::Error> {
    let mut s = String::new();
    File::open("hello.txt")?.read_to_string(&mut s)?;
    Ok(s)
}
```

### Testing

```rust
// Unit tests
#[cfg(test)]
mod tests {
    #[test]
    fn my_unit_test() {
        let my_res = my_add_function(1, 2);
        assert_eq!(my_res, 3)
    }
}
```

### Modules

```rust
// A collection of items: functions, structs, traits, impl blocks, and other modules
mod my_mod {
    fn my_private_function() {
        // ...
    }

    pub fn my_public_function() {
        // ...
    }

    pub struct MyPublicStruct {
        // ...
    }
}

// absolute path
use crate::my_crate::my_function(); // referring to an item in the module tree

// relative path
self::my_function(); // current module scope
super::my_function(); // parent scope

// external crate
use std::io;

// renaming external crate
use futures as f;
use self::f::Future;

// submodules
foo.rs // module
foo/bar.rs // submodule
```

### Crates

```bash
# A tree of modules that produces a library or executable
cargo new --lib my-lib # create library crate
cargo new --bin my-bin # create binary crate
```

### Packages

```bash
# A Cargo feature that lets you build, test, and share crates
cargo new my-project
```

### External packages (Cargo.toml)

```toml
[dependencies]
package_name = "^1.2.3" # < 2.0.0 (caret)
package_name = "~1.2.3" # < 1.3.0 (tilde)
package_name = "1.2.*" # < 1.3.0 (wildcard)
package_name = "*" # > 0.0.0
```

### Cargo (package manager)

```bash
cargo --version
cargo fmt # Format source code
cargo check # Validate source code
cargo run
cargo run --release
cargo test
cargo build # Compile source code
cargo build --release
cargo clean
```

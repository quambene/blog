<!-- markdownlint-disable MD001 -->

# Python

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Error handling](#error-handling)

### Print

```python
name = "world"
print("Hello", name)
print(f"Hello, {name}!")
print("This %(verb)s a %(noun)s." % {"noun": "test", "verb": "is"})
print("integer: %d float: %f" % (my_int, my_float))
```

### Variables

```python
x: int # Declare type
x = 4 # Assign value
x: int = 4 # Assign value (typed)
x = y = z = 0 # Multiple assignment
x += 1 # Increment
x -= 1 # Decrement
```

### Data types

```python
# Basic types
x: int
x: float
x: complex
x: str
x: bool

# List
x = ["item1", "item2", "item3"]
x: List[str] = ["item1", "item2", "item3"] # typed
x[0:3] # Indexing is inclusive-exclusive
x[-3:-1] # Negative indexes count from the last item backwards

# Tuple
x = (1, 2, 3)
x: Tuple[int, int, int] = (1, 2, 3) # typed

# Dictionary
x = {"key1": 1, "key2": 2}
x: Dict[int, int] = {"key1": 1, "key2": 2} # typed

# Option
x: Optional[str] = some_function()
```

### Control flow

```python
# for loop
for i in range(10):
    print(i)

# while loop
while i < 3:
    print(i)

# if-else
if a < b:
    # statement
elif a == b:
    # statement
else:
    # statement
```

### Functions

```python
def my_function(arg, optional_arg = 'default value'):
    return arg, optional_arg

# Typed function
def my_function(arg1: int, arg2: int) -> Tuple[int, int]:
    return arg1, arg2

# Lambda function
add_one = lambda x: x + 1

# Decorator
@my_decorator
def my_function():
    return
```

### Classes

```python
class MyClass:
    my_class_var = 100

    def __init__(self):
        self.my_instance_var = 3

    def my_function(self):
        return self.my_instance_var

# Instantiation
my_class_instance = MyClass()
my_class_instance.my_function()
my_class_instance.my_class_var

# Data class
@dataclass
class User:
    name: str
    email: str
```

### Error handling

```python
try:
    # statement
except ZeroDivisionError: # if an exception was raised in the try clause
    # statement
else: # if no exceptions were raised in the try clause
    # statement
finally: # always executed
    # statement

# Raise error
raise ValueError("error message")
```

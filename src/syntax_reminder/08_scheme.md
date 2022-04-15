<!-- markdownlint-disable MD001 -->

# Scheme

### Prefix notation

```haskell
;;; Combination
(+ 5 64)

;;; Fundamental forms
define
lambda
set!
```

### Print

```haskell
(write-line "hello world")
```

### Variables

```haskell
(define pi 3.14159)

(define string "my string")

;;; Local state variables
(set! <name> <new-value>)
```

### Data types

```haskell
;;; List
(list 1 2 3 4)
```

### Procedure

```haskell
(define (square x) (* x x))

;;; Lambda
(lambda (x) (+ x 4))
```

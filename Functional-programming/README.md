# Notes from the course of Functional Programming at FMI 2021/2022
### Literature
 - Structure and Interpretation of Computer Programs
 - How to Design Programs: An Introduction to Computing

### Expressions
2 types of expressoons:
 - Primitive/atomic -> numbers, strings etc
 - Combinations -> function calls
There are special cases like `define`. They obey different reduction rules.

#### Function call syntax
In this context function == procedure
```lisp
(<name-of-function> [<arg_1> <arg_2> <arg_3> ... <arg_n>])
```

#### Define procedure
```lisp
(define <name> <expr>)
```
Associates name with the value of expression **in the current environment**

### Data structures - 2021-11-03
Simplest possible case:
```lisp
(define l (cons 1 2))

(car l) ;; => 1
(cdr l) ;; => 2
```
They can be nested:
```lisp
(define l (cons (cons 1 2) (cons 3 4)))

(car l) ;; => (1 2)
(cdr l) ;; => (3 4)

(car (car l)) ;; => 1
(cdr (car l)) ;; => 2
(car (cdr l)) ;; => 3
(cdr (cdr l)) ;; => 4
```
They can be heterogeneous:
```lisp
(cons (cons 1 (cons 2 3)) 4) ;; => ((1 (2 3)) 4)
```

### S-expressions
**S**ymbolic **expressions** are:
 - Atomic expressions - numbers, `#t`, `#f`, etc.
 - Symbolic atoms - indentifiers
 - There are **no** other S-expressions

##### Quotations
```lisp
(quote <S-expr>)
'(<S-expr>) ;; note the ' at the front
```
Causes the given s-expr to be passed along and not evaluated

##### Checking functions:
```lisp
pair?   ;; <= checks if the given s-expr is a pair (do I really have to explain it tho...)
list?   ;; <= ----------- | | ------------- a list
number? ;; <= ----------- | | ------------- a number
symbol? ;; <= ----------- | | ------------- an indentifier
string? ;; <= ----------- | | ------------- a string
```

### Lists
Finally, considering LISP == **Lis**t **P**rocessing. Internally they are most probably implemented using pairs where the first value is an element of the list and the second is the tail of the list. Seems it is recursively defined, how convenient:
 - Base: there is an empty list: `'()`
 - A list is constructed by adding an element `el` at the front of the list `l`: `(cons el l)`
`(cons el l)` trully produces `(el l) => (el (el2 tail2)) => ... => (el (el2 (el3 (... (eln ())...))))`, for convenience LISP reduces it to: `(el1 el2 el3 ... eln)`

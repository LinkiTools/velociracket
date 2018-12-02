# velociracket

A Racket Racket-like language to write high performance programs.

## Idea

The idea of velociracket is to explore how much of Racket you can
implement, and how many constraints you need to impose to allow
generate really fast code.

`velociracket` is going to be implemented as a racket language that,
at least, initially compiled to C but interoperates seemlessly with
other racket languages. I would hope for it to look exactly like
racket but if, for the sake of performance, some constraints are
required then they shall be inserted.

The user writes something like 

```racket
#lang velociracket

(define (foo x)
  (printf "Hello from velociracket~n")
  (+ x 1))
  
(foo 2)
```

Something like this would happen:

```racket
Hello from velociracket
3
```

The string comes from the standard output and the `3` is the result
value of calling `(foo 2)`.

In the background all code converted to C, compiled into a dynamic
library, and FFI bindings are automatically generated and exported if
any of the values are provided.

## Reader and Expander  

Since we use S-expressions already we don't need to implement a new reader. Instead we use the normal syntax reader (`read-syntax`) and then we implement the expander.

The expander needs to 
1. Convert the syntax to C;
2. Compile the C into a dll;
3. Generate C FFI syntax to interoperate with Racket

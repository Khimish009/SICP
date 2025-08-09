---
title: "SICP - Solution: Exercise 1.34"
date: 2025-08-09T13:33:22.836Z
---

## Exercise 1.34

> Suppose we define the procedure
> 
> ```scheme
> (define (f g) (g 2))
> ```
> 
> Then we have
> 
> ```scheme
> (f square)
> 4
> 
> (f (lambda (z) (* z (+ z 1))))
> 6
> ```
> 
> What happens if we (perversely) ask the interpreter to evaluate the combination `(f f)`? Explain.

## Solution

The trace for the evaluation of `(f f)` will be:

```scheme
(f f)
(f 2)
(2 2)
```

And will fail, since `2` is not an function that can be applied.

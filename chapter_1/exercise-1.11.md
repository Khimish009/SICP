---
title: "SICP - Solution: Exercise 1.11"
date: 2025-06-24T10:48:54.039Z
---

## Exercise 1.11

> A function $f$ is defined by the rule that ${f(n)=n}$ if ${n<3}$ and
${f(n)}={f(n-1)}+{2f(n-2)}+{3f(n-3)}$ if ${n\geq3}$.
> 
> Write a procedure that computes f by means of a recursive process. Write a procedure that computes f by means of an iterative process.

## Solution

Recursive version:

```scheme
(define (f-recursive n)
  (if (< n 3)
      n
      (+ (f-recursive (- n 1)) (f-recursive (- n 2)) (f-recursive (- n 3)))))
```

Iterative version:

```scheme
(define (f-iterative n)
  (define (fn-loop a b c count)
  (if (< count 3) a
      (fn-loop (+ a b c) a b (- count 1))))

  (if (< n 3)
      n
      (fn-loop 2 1 0 n)))

```

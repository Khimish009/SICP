---
title: "SICP - Solution: Exercise 1.27"
date: 2025-07-09T09:20:54.258Z
---

## Exercise 1.27

> Demonstrate that the Carmichael numbers listed in Footnote 47 really do fool the Fermat test. That is, write a procedure that takes an integer $n$ and tests whether an is congruent to $a$ modulo $n$ for every ${a<n}$, and try your procedure on the given Carmichael numbers.

## Solution

Let's just run the number and see:

```scheme
(define (square x) (* x x))

(define (expmod base exp m)
  (cond ((= exp 0) 1)
        ((even? exp)
         (remainder
          (square (expmod base (/ exp 2) m))
          m))
        (else
         (remainder
          (* base (expmod base (- exp 1) m))
          m))))


(define (carmichael-test n)
  (define (carmichael-test-iter n a)
    (cond
      [(= a n) #t]
      [(= (expmod a n n) a) (carmichael-test-iter n (+ a 1))]
      [else #f]))
  
  (carmichael-test-iter n 1))

(define carmichaels
  '(561 1105 1729 2465 2821 6601 8911 10585 15841 29341
    41041 46657))

(map carmichael-test carmichaels)
```

Evaluates to:

```
(#t #t #t #t #t #t #t #t #t #t #t #t)
```

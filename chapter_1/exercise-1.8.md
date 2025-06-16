---
title: "SICP - Solution: Exercise 1.8"
date: 2025-06-16T16:56:45.298Z
---

## Exercise 1.8

> Newton’s method for cube roots is based on the fact that if $y$ is an approximation to the cube root of $x$, then a better approximation is given by the value
>
> $${\frac{{x/y^2}+2y}3.}$$
>
> Use this formula to implement a cube-root procedure analogous to the square-root procedure. (In 1.3.4 we will see how to implement Newton’s method in general as an abstraction of these `square-root` and `cube-root` procedures.)

## Solution

Using the same improvement for large and small number from exercise 1.7:

```scheme
(define (cube x) (* x x x))

(define (good-enough? previous-guess guess)
  (< (abs (/ (- guess previous-guess) guess)) 0.00000000001))

(define (cube-root-iter guess x)
  (if (good-enough? (improve guess x) guess)
      guess
      (cube-root-iter (improve guess x) x)))

(define (improve guess x)
  (/ (+ (/ x (* guess guess)) (* 2 guess)) 3))


(define (cube-root x)
  (cube-root-iter 1.0 x))

; Basic testing
(define x 12345)
(define cube-root-x (cube-root x))
(newline)
(display "(cube-root ") (display x) (display ") -> ") (display cube-root-x)
(newline)
(display "(cube ") (display cube-root-x) (display ") -> ") (display (cube cube-root-x))
```

Returns:

```
(cube-root 12345) -> 23.111618749807374
(cube 23.111618749807374) -> 12345.000000000167
```

---
title: "SICP - Solution: Exercise 1.22"
date: 2025-07-07T13:12:52.910Z
---

## Exercise 1.22

> Most Lisp implementations include a primitive called `runtime` that returns an integer that specifies the amount of time the system has been running (measured, for example, in microseconds). The following `timed-prime-test` procedure, when called with an integer $n$, prints $n$ and checks to see if $n$ is prime. If $n$ is prime, the procedure prints three asterisks followed by the amount of time used in performing the test.
> 
> ```scheme
> (define (timed-prime-test n)
>   (newline)
>   (display n)
>   (start-prime-test n (runtime)))
> (define (start-prime-test n start-time)
>   (if (prime? n)
>       (report-prime (- (runtime)
>                        start-time))))
> (define (report-prime elapsed-time)
>   (display " *** ")
>   (display elapsed-time))
> ```
> 
> Using this procedure, write a procedure `search-for-primes` that checks the primality of consecutive odd integers in a specified range. Use your procedure to find the three smallest primes larger than 1000; larger than 10,000; larger than 100,000; larger than 1,000,000. Note the time needed to test each prime. Since the testing algorithm has order of growth of ${\mathrm\Theta(\sqrt n)}$, you should expect that testing for primes around 10,000 should take about $\sqrt {10}$ times as long as testing for primes around 1000. Do your timing data bear this out? How well do the data for 100,000 and 1,000,000 support the ${\mathrm\Theta(\sqrt n)}$ prediction? Is your result compatible with the notion that programs on your machine run in time proportional to the number of steps required for the computation?

## Solution

Since `runtime` is not part of DrRacket, you can use [current-inexact-milliseconds](https://docs.racket-lang.org/reference/time.html#%28def._%28%28quote._~23~25kernel%29._current-inexact-milliseconds%29%29). The code, including the `search-for-primes` function is:

```scheme
(define (square x) (* x x))

(define (even? n)
  (= (remainder n 2) 0))

(define (runtime)
  (current-inexact-milliseconds))

(define (prime? n)
(= n (smallest-divisor n)))

(define (smallest-divisor n)
  (find-divisor n 2))

(define (find-divisor n test-divisor)
  (cond ((> (square test-divisor) n) n)
        ((divides? test-divisor n) test-divisor)
        (else (find-divisor n (+ test-divisor 1)))))

(define (divides? a b)
  (= (remainder b a) 0))

(define (search-for-primes L start-time)
  (define (search-for-primes-iter n times)
    (cond [(= times 0) (- (runtime) start-time)]
          [(even? n) (search-for-primes-iter (+ n 1) times)]
          [(prime? n) (search-for-primes-iter (+ n 1) (- times 1))]
          [else (search-for-primes-iter (+ n 1) times)]
          ))

  (search-for-primes-iter L 3))

(search-for-primes 1000 (runtime)) ; 0.008056640625
(search-for-primes 10000 (runtime)) ; 0.026123046875
(search-for-primes 100000 (runtime)) ; 0.052001953125
(search-for-primes 1000000 (runtime)) ; 0.1171875
```

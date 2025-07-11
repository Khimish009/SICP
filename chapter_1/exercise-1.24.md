---
title: "SICP - Solution: Exercise 1.24"
date: 2025-07-08T15:15:34.833Z
---

## Exercise 1.24

> Modify the `timed-prime-test` procedure of Exercise 1.22 to use `fast-prime?` (the Fermat method), and test each of the 12 primes you found in that exercise. Since the Fermat test has ${\mathrm\Theta(\log n)}$ growth, how would you expect the time to test primes near 1,000,000 to compare with the time needed to test primes near 1000? Do your data bear this out? Can you explain any discrepancy you find?

## Solution

```scheme
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

(define (fermat-test n)
  (define (try-it a)
    (= (expmod a n n) a))
  (try-it (+ 1 (random (- n 1)))))

(define (fast-prime? n times)
  (cond ((= times 0) #t)
        ((fermat-test n)
         (fast-prime? n (- times 1)))
        (else #f)))
```

### Conclusion

 Calculation results (all provided numbers were taken):

 1009 *** 0.026611328125  
 1013 *** 0.0341796875  
 1019 *** 0.041015625  
 1021 *** 0.037109375  
 1031 *** 0.04345703125  
 1033 *** 0.0439453125  
 1039 *** 0.034912109375  
 1049 *** 0.038818359375  
 1051 *** 0.035400390625 
 1061 *** 0.0400390625  
 1063 *** 0.038330078125  
 1069 *** 0.036376953125  

 10007 *** 0.043212890625  
 10009 *** 0.035888671875  
 10037 *** 0.038330078125  
 10039 *** 0.045654296875  
 10061 *** 0.055419921875  
 10067 *** 0.044189453125  
 10069 *** 0.047119140625  

 100003 *** 0.053466796875  
 100019 *** 0.05810546875  
 100043 *** 0.05908203125  
 100049 *** 0.0546875  
 100057 *** 0.074951171875  
 100069 *** 0.049072265625  

 1000003 *** 0.0625  
 1000033 *** 0.062744140625  
 1000037 *** 0.063720703125  
 1000039 *** 0.065673828125  
 1000081 *** 0.06298828125  

 Execution Time Analysis:  

 1. For numbers around 1000:  
    - Average checking time: 0.038087 seconds  
    - In the previous task: 0.000244 seconds  
    - Time ratio: 156.92 

 2. For numbers around 10,000:  
    - Average checking time: 0.044631 seconds  
    - In the previous task: 0.000683 seconds  
    - Time ratio: 65.34  

 3. For numbers around 100,000:  
    - Average checking time: 0.058894 seconds  
    - In the previous task: 0.001458 seconds  
    - Time ratio: 40.41  

 4. For numbers around 1,000,000:  
    - Average checking time: 0.063525 seconds  
    - In the previous task: 0.004598 seconds  
    - Time ratio: 13.81  

 Conclusion:  

 Introducing the Fermat primality test led to significant changes in execution time:  

 1. For numbers around 1000, time increased by a factor of 156.92.  
 2. For numbers around 10,000, time increased by a factor of 65.34.  
 3. For numbers around 100,000, time increased by a factor of 40.41.   
 4. For numbers around 1,000,000, time increased by a factor of 13.81.  

These results show that while the Fermat test has a complexity of Θ(log n), as expected, the observed time ratios indicate that for smaller numbers, the Fermat method leads to a significant increase in checking time, while for larger numbers, this increase is less noticeable.  

Comparison with the order of growth conclusion:  

When the size of the number increases by an order of magnitude (10 times), the prime? method requires approximately 3 times more computation, confirming a linear time increase. Meanwhile, the fast-prime? method shows almost constant time increase, confirming its logarithmic order of growth. This means that as the number size increases by an order of magnitude, the fast-prime? method requires only a constant increase in time. Thus, while the prime? method is faster for small numbers, the fast-prime? method becomes significantly faster for larger numbers.  

When the size of `prime` is 10 times larger, `prime?` requires around 3 times more computation.  

When the size of  `prime` is 10 times larger, `fast-prime?` require only a constant increase of time (around 50µs on my computer). ${\mathrm\Theta(\log n)}$ growth means that when the prime are ten times larger, the time will increase by a constant amount ${\log(100)-\log(10)=1}$. This is quite clear here.

Although for smaller number `prime?` is faster, `fast-prime?` become much faster with larger and larger prime.

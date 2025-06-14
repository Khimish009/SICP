---
title: "SICP - Solution: Exercise 1.2"
date: 2025-06-14T11:43:42.256Z
---

## Exercise 1.2

> Translate the following expression into prefix form:
> 
> $${\frac{5+4+(2-(3-(6+\frac45)))}{3(6-2)(2-7)}.}$$

## Solution

```scheme
(/ (+ 5
      4
      (- 2
         (- 3
            (+ 6
               (/ 4 5)))))
   (* 3
      (- 6 2)
      (- 2 7)))
```

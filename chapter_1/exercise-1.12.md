---
title: "SICP - Solution: Exercise 1.12"
date: 2025-06-24T11:53:11.434Z
---

## Exercise 1.12

> The following pattern of numbers is called Pascal’s triangle.
> 
> ```
>          1
>        1   1
>      1   2   1
>    1   3   3   1
>  1   4   6   4   1
>        . . .
> ```
> 
> The numbers at the edge of the triangle are all 1, and each number inside the triangle is the sum of the two numbers above it. Write a procedure that computes elements of Pascal’s triangle by means of a recursive process.

## Solution

The solution is easier to understand if you change slightly the tabulation:

```
 1
 1   1
 1   2   1
 1   3   3   1
 1   4   6   4   1
       . . .
```

From the definition given, the function to compute a single number at a given position can be defined recursively:

```scheme
(define (pascal row col)
  (cond ((= row 1) 1)
        ((or (= col 1) (= col row)) 1)
        (else (+ (pascal (- row 1)  (- col 1))
                 (pascal (- row 1) col)))))
```

Using this function, we write a couple more functions to display the triangle:

```scheme
(define (display-pascal-row n)
  (define (column-iter i)
    (display (pascal n i)) (display "  ")
    (if (= i n)
        (newline)
        (column-iter (+ i 1))))
  (column-iter 1))

(define (display-pascal n)
  (define (display-pascal-iter i)
    (display-pascal-row i)
    (if (= i n)
        (newline)
        (display-pascal-iter (+ i 1))))
  (display-pascal-iter 1))
```

To check our solution, we can evaluate `(display-pascal 14)`:

```
1  
1  1  
1  2  1  
1  3  3  1  
1  4  6  4  1  
1  5  10  10  5  1  
1  6  15  20  15  6  1  
1  7  21  35  35  21  7  1  
1  8  28  56  70  56  28  8  1  
1  9  36  84  126  126  84  36  9  1  
1  10  45  120  210  252  210  120  45  10  1  
1  11  55  165  330  462  462  330  165  55  11  1  
1  12  66  220  495  792  924  792  495  220  66  12  1  
1  13  78  286  715  1287  1716  1716  1287  715  286  78  13  1  
```

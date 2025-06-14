---
title: "SICP - Solution: Exercise 1.4"
date: 2025-06-14T12:36:11.829Z
---

## Exercise 1.4

> Observe that our model of evaluation allows for combinations whose operators are compound expressions. Use this observation to describe the behavior of the following procedure:
> 
> ```scheme
> (define (a-plus-abs-b a b)
>   ((if (> b 0) + -) a b))
> ```

## Solution

If $b$ is strictly a positive number, the operator expression `(if (> b 0) + -)` will evaluate to the primitive procedure `+`, the expression then becomes `(+ a b)` and the result will be $a+b$. 

In all other cases, when $b$ is a negative number, `(if (> b 0) + -)` will evaluate to the primitive procedure `-`, the expression then becomes `(- a b)` and the result will evaluate to $a-b$.

This function compute $a+\left|b\right|$.

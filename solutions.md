---
author: Cezar
lang: en
title: 99 Lisp Problems and Solutions
---

-   [99 Lisp problems](#lisp-problems){#toc-lisp-problems}
    -   [Problem 01 - Find the last box of a
        list.](#problem-01---find-the-last-box-of-a-list.){#toc-problem-01---find-the-last-box-of-a-list.}
    -   [Problem 02 - Find the last, but one, box of a
        list.](#problem-02---find-the-last-but-one-box-of-a-list.){#toc-problem-02---find-the-last-but-one-box-of-a-list.}
    -   [Problem 03 - Find the K\'th element of a list. (1 based
        index)](#problem-03---find-the-kth-element-of-a-list.-1-based-index){#toc-problem-03---find-the-kth-element-of-a-list.-1-based-index}
    -   [Problem 04 - Find the numbers of elements on a
        list.](#problem-04---find-the-numbers-of-elements-on-a-list.){#toc-problem-04---find-the-numbers-of-elements-on-a-list.}
    -   [Problem 05 - Reverse a
        list.](#problem-05---reverse-a-list.){#toc-problem-05---reverse-a-list.}

# 99 Lisp problems

<https://www.ic.unicamp.br/~meidanis/courses/mc336/problemas-lisp/L-99_Ninety-Nine_Lisp_Problems.html>

Focus on recursion and try to only use the most basic builtin functions
to solve the given problems. As the problems become more complex you can
allow yourself to use more builtins.

## Problem 01 - Find the last box of a list.

**Example:** (fn \'(A B C D)) -\> (D)

``` {#problem-01 .commonlisp org-language="emacs-lisp" results="raw"}
(defun my-last(LIST)
  "Returns the last box of a list"
  (if (cdr LIST) (if (cdr (cdr LIST)) (my-last (cdr LIST)) (cdr LIST)) LIST))

;; Test evaluations
(format "%s\n%s\n%s\n%s\n%s\n%s\n"
        (my-last '(A B C D))
        (my-last '(A))
        (my-last '(A B))
        (my-last '(A B C))
        (my-last '(A B (C D)))
        (my-last '(A B (C (D E)) F)))
```

```{=org}
#+RESULTS: problem-01
```
\(D\) (A) (B) (C) ((C D)) (F)

## Problem 02 - Find the last, but one, box of a list.

**Example:** (fn \'(A B C D)) -\> (C D)

``` {#problem-02 .commonlisp org-language="emacs-lisp" results="raw"}
(defun my-last-but-one(LIST)
  "Returns the last but one box of a list"
  (if (>= (length (cdr LIST)) 2) (my-last-but-one (cdr LIST)) LIST))

;; Test evaluations
(format "%s\n%s\n%s\n%s\n%s\n%s\n"
        (my-last-but-one '(A B C D))
        (my-last-but-one '(A))
        (my-last-but-one '(A B))
        (my-last-but-one '(A B C))
        (my-last-but-one '(A B (C D)))
        (my-last-but-one '(A B (C (D E)) F)))
```

```{=org}
#+RESULTS: problem-02
```
(C D) (A) (A B) (B C) (B (C D)) ((C (D E)) F)

## Problem 03 - Find the K\'th element of a list. (1 based index)

**Example:** (fn \'(A B C D) 3) -\> C

``` {#problem-03 .commonlisp org-language="emacs-lisp" results="raw"}
(defun my-nth-element(LIST N)
  "Returns the nth element of a list"
  (if (<= N 1) (car LIST) (my-nth-element (cdr LIST) (- N 1))))

;; Test evaluations
(format "%s\n%s\n%s\n%s\n%s\n%s\n"
        (my-nth-element '(A B C D) 3)
        (my-nth-element '(A) 1)
        (my-nth-element '(A B) 1)
        (my-nth-element '(A B C) 2)
        (my-nth-element '(A B (C D)) 3)
        (my-nth-element '(A B (C (D E)) F) 3))
```

```{=org}
#+RESULTS: problem-03
```
C A A B (C D) (C (D E))

## Problem 04 - Find the numbers of elements on a list.

**Example:** (fn \'(A B C D)) -\> 4

``` {#problem-04 .commonlisp org-language="emacs-lisp" results="raw"}
(defun my-num-of-elements(LIST)
  "Returns the number of elements on a list"
  (if (cdr LIST) (+ (my-num-of-elements (cdr LIST)) 1) 1))

;; Test evaluations
(format "%s\n%s\n%s\n%s\n%s\n%s\n"
        (my-num-of-elements '(A B C D))
        (my-num-of-elements '(A))
        (my-num-of-elements '(A B))
        (my-num-of-elements '(A B C))
        (my-num-of-elements '(A B (C D)))
        (my-num-of-elements '(A B (C (D E)) F)))
```

```{=org}
#+RESULTS: problem-04
```
4 1 2 3 3 4

## Problem 05 - Reverse a list.

**Example:** (fn \'(A B C D)) -\> (D C B A)

``` {#problem-05 .commonlisp org-language="emacs-lisp" results="raw"}
(defun my-reverse-list(LIST)
  "Reverses a list"
  (if (cdr LIST) (append (last LIST) (my-reverse-list (butlast LIST))) LIST))

;; Test evaluations
(format "%s\n%s\n%s\n%s\n%s\n%s\n"
        (my-reverse-list '(A B C D))
        (my-reverse-list '(A))
        (my-reverse-list '(A B))
        (my-reverse-list '(A B C))
        (my-reverse-list '(A B (C D)))
        (my-reverse-list '(A B (C (D E)) F)))
```

```{=org}
#+RESULTS: problem-05
```
(D C B A) (A) (B A) (C B A) ((C D) B A) (F (C (D E)) B A)

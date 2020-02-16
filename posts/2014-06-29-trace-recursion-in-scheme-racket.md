---
title: Trace Recursion in Scheme / Racket
date: 2014-06-29
path: "/blog/trace-recursion-in-scheme-racket/"
---

The topic of tracing recursion in Scheme came up at today's SICP study group meeting. It can be done with Dr. Racket.

Here are the relevant <a href="http://docs.racket-lang.org/reference/debugging.html">docs</a>.

First require trace:

<code>(require racket/trace)</code>

Then trace the function that uses recursion:
<code>(trace cc)</code>

A complete example from SICP:

```
(define (count-change amount)
  (cc amount 5))

(define (cc amount kinds-of-coins)
  (cond ((= amount 0) 1) ; If 0 return 1
    ((or (< amount 0) (= kinds-of-coins 0)) 0) ; If nothing to do return 0
    (else (+ (cc amount (- kinds-of-coins 1))
    (cc (- amount (first-denomination kinds-of-coins)) kinds-of-coins)))))

(define (first-denomination kinds-of-coins)
  (cond ((= kinds-of-coins 1) 1)
    ((= kinds-of-coins 2) 5)
    ((= kinds-of-coins 3) 10)
    ((= kinds-of-coins 4) 25)
    ((= kinds-of-coins 5) 50)))
```

Trace:

```text
> (trace cc)
> (count-change 10)
>(cc 10 5)
> (cc 10 4)
> >(cc 10 3)
> > (cc 10 2)
> > >(cc 10 1)
> > > (cc 10 0)
< < < 0
> > > (cc 9 1)
> > > >(cc 9 0)
< < < <0
> > > >(cc 8 1)
> > > > (cc 8 0)
< < < < 0
> > > > (cc 7 1)
> > > > >(cc 7 0)
< < < < <0
> > > > >(cc 6 1)
> > > > > (cc 6 0)
< < < < < 0
> > > > > (cc 5 1)
> > > >[10] (cc 5 0)
< < < <[10] 0
> > > >[10] (cc 4 1)
> > > >[11] (cc 4 0)
< < < <[11] 0
> > > >[11] (cc 3 1)
> > > >[12] (cc 3 0)
< < < <[12] 0
> > > >[12] (cc 2 1)
> > > >[13] (cc 2 0)
< < < <[13] 0
> > > >[13] (cc 1 1)
> > > >[14] (cc 1 0)
< < < <[14] 0
> > > >[14] (cc 0 1)
< < < <[14] 1
< < < <[13] 1
< < < <[12] 1
< < < <[11] 1
< < < <[10] 1
< < < < < 1
< < < < <1
< < < < 1
< < < <1
< < < 1
< < <1
> > >(cc 5 2)
> > > (cc 5 1)
> > > >(cc 5 0)
< < < <0
> > > >(cc 4 1)
> > > > (cc 4 0)
< < < < 0
> > > > (cc 3 1)
> > > > >(cc 3 0)
< < < < <0
> > > > >(cc 2 1)
> > > > > (cc 2 0)
< < < < < 0
> > > > > (cc 1 1)
> > > >[10] (cc 1 0)
< < < <[10] 0
> > > >[10] (cc 0 1)
< < < <[10] 1
< < < < < 1
< < < < <1
< < < < 1
< < < <1
< < < 1
> > > (cc 0 2)
< < < 1
< < <2
< < 3
> > (cc 0 3)
< < 1
< <4
> >(cc -15 4)
< <0
< 4
> (cc -40 5)
< 0
<4
4
>
```

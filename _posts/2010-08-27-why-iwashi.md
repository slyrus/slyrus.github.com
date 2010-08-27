---
layout: post
title: Iwashi -- packed arrays in clojure
---

{{ page.title }}
================

<p class="meta">27 August 2010 - Bolinas</p>

One thing that I miss from Common Lisp in clojure is efficient support
for elements of arbitrary, fixed types, such as integers within a
given range. Yes, clojure does have support for arrays of booleans,
bytes, chars, ints, shorts, longs, floats, doubles, and objects, but
there is no explicit, efficient support for 2-, 4- and 5- bit
integers. Even the 8-bit type (bytes) are really signed bytes, so
there's no nice, effecient, built-in storage for quantities in the
range 0-255. Why would one want 2-bit integers? Well, if you want to
store the 3 billion bases of the human genome in RAM, you're going to
use a lot less RAM to do so if you can pack 4 bases into each byte,
rather than 1, or, worse yet, 1 base per 2-bytes if you use
char-arrays.

Enter iwashi (Japanese for sardine, I think -- at least that's what
they call it at the sushi counter). Iwashi provides for efficient
storage of 2-, 4- and 5-bit integers in clojure arrays. There are 6
main functions that one calls to use Iwashi. Three functions for
creating iwashi arrays:

* make-2-bit-array
* make-4-bit-array
* make-5-bit-array

And three functions for using the arrays:

* length
* item
* set-item

To use, make sure iwashi is on the classpath and do, for instance:

    (require '[iwashi.array :as array])

For example, let's make a 2-bit array with 128 items in it and the
first 32 items to the item's index modulo 4:

    (let [q (array/make-2-bit-array (bigint 128))]
      (doall (map #(array/set-item q % (mod % 4))
                  (take 32 (iterate inc 0))))
      (map #(array/item q %)
           (take 32 (iterate inc 0))))
    => (0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3)

Now for a bigger, trivial, example, let's make a 4,000,000,000
element 2-bit array and set the first 32 values of it:

    (let [q (array/make-2-bit-array (bigint 4e9))]
      (doall (map #(array/set-item q (+ (bigint 3e9) %) (mod % 4))
                  (take 32 (iterate inc 0))))
      (map #(array/item q (+ (bigint 3e9) %))
           (take 32 (iterate inc 0))))
    => (0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3 0 1 2 3)

In another post, we'll load some DNA and protein sequences into
packed arrays just for fun.

Enjoy.

--


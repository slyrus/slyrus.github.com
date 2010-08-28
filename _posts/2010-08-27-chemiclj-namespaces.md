---
layout: post
title: chemiclj clojure ns'es 
---

{{ page.title }}
================

<p class="meta">27 August 2010 - Bolinas</p>

One problem that I've run into with clojure in trying to write
chemiclj is the issue of how to structure/organize the code such that
things are arranged neatly and cleanly, and that the various bits of
code get loaded in the proper order. One solution to this is to just
have everything in a single file and make sure that the forms appear
in the proper order. On the
[ns-hackery](http://github.com/slyrus/chemiclj/tree/ns-hackery) branch I've
split things up into multiple files, and, as seems to be the clojure
idiom, multiple ns'es, one per file. The problem that this presents
for me is that I want to present a clean interface to other pieces of
code. If we put the protocol functions in chemiclj.core and make sure
that the other files :use/:require core, such that they can get access
to the protocol functions, we can't define functions that need access
to the record types that will be created with defrecord in the other
files, such as the Molecule record-type which will be created in
molecule.clj.

Similarly, I can't define the record types first, because they need
access to the protocol functions. The order in which things get
evaluated seems like it needs to be: protocols, records (or other
concrete implementations of the protocols), and then functions that
use these records, for instance constructor and helper functions. This
isn't a problem if one is comfortable having the records and the
constructor/helper functions in the same class. In that case one can
just define the protocol types in, say, chemiclj.core and the put the
defrecord forms and the constructor/helper functions in, say,
chemiclj.molecule. BUT if you want to have the constructor and helper
functions in chemiclj.core, and yet have the defrecord in
chemiclj.molecule, it seems like you're out of luck.

There are probably many different ways to address this. The simplest
is just to have the code live in multiple packages and have folks
:use/:require those packages, as neccessary:

    (ns chemiclj-scratch
      (:use [chemiclj core atom bond molecule]))


But, if one would prefer to :require :as the package, like:

    (ns chemiclj-scratch
      (:require [chemiclj.core :as chem]))

you won't get access to the constructor/functions for molecule unless you do:

    (ns chemiclj-scratch
      (:require [chemiclj.core :as chem]
                [chemiclj.atom :as atom]
                [chemiclj.molecule :as molecule]))

And then you have to remember to do:

    (atom/make-atom "H" "H1")
    ...

Which gets tedious. So, what do we do? Well, we could try adding some
in-ns forms at the end of the implementation files, but the problem
with this is that these won't necessarily get loaded if one does:

    (require '[chemiclj [core :as chem]])

So, I think we need to do that and do:

    (load "atom")
    (load "molecule")

at the end of core.clj. But, rather than do the (in-ns ...) trick, what if we could just do:

    (defn chemiclj.core/make-atom ...)

Well, the problem with this is that we can't. The compiler complains
about trying to define things that aren't in teh current ns. Yet
intern should still allow us to do this. Some quick macro-hackery
gives us:

    (defmacro defn* [fn-name & rest]
      `(intern (if ~(namespace fn-name)
                 (symbol ~(namespace fn-name))
                 (ns-name *ns*))
               (symbol ~(name fn-name)) (fn ~(symbol (name fn-name)) ~@rest)))

And then we can do:

    (defn* chemiclj.core/make-atom [element name & {:keys [isotope chirality charge
                                                       hybridization aromatic
                                                       explicit-hydrogen-count]
                                                :or {charge 0}}]
      ...)

for instance, and things seem good. One wrinkle is that if we want to
do this with a recursive function, we better make sure we call the
function in the right package:

    (defn* chemiclj.core/remove-atoms-of-element [mol element]
      (reduce (fn [mol atom]
                (remove-atom mol atom))
              mol
              (chemiclj.core/get-atoms-of-element mol element)))

All of this is a lot of work and nasty hackery to avoid either
:use'ing core molecule and atom, or calling atom/make-atom, but it's
been an interesting exercise in learning how clojure thinks about
namespaces. Perhaps I'll think better of this and back it out, but for
the moment, it makes for a clean interface to a rich(er) chemiclj.core
package.

Note: all of the code for this is now on [ns-hackery branch of
chemiclj](http://github.com/slyrus/chemiclj/tree/ns-hackery).


--


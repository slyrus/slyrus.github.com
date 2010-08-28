---
layout: post
title: Getting started with chemiclj
---

{{ page.title }}
================

<p class="meta">27 August 2010 - Bolinas</p>

[chemiclj](http://github.com/slyrus/chemiclj) is a library for
representing and processing various kinds of chemical entities, such
as elements, atoms, bonds and molecules. To see chemiclj in action,
let's build a model of methane (we'll see later how to do this less
tediously). But first, a word about clojure programming style. Coming
from a background in Java, C++, Common Lisp, etc..., one might expect
that to build a model of methane, you create a molecule object, and
then add atoms and bonds to it. While that's smililar to what one does
in clojure (in indeed can do with clojure using the mutable data types
and their operators), the clojur-ish thing to do seems to be to create
new objects at each step along the way, rather than mutating the
existing objects. Therefore, we create a molecule object, and, say,
add a carbon to it, but instead of receiving the same object, modified
in place, we receive a new object with the carbon in it. So, to build
up a molecule like methane one would do:

    (require '[chemiclj [core :as chem]])
    ;=> nil
    
    
    (def ethane
         (let [c1 (chem/make-atom "C" "C1")
               h1 (chem/make-atom "H" "H1")
               h2 (chem/make-atom "H" "H2")
               h3 (chem/make-atom "H" "H3")
               h4 (chem/make-atom "H" "H4")]
           (chem/add-bond
            (chem/add-bond
             (chem/add-bond
              (chem/add-bond
               (chem/add-atom
                (chem/add-atom
                 (chem/add-atom
                  (chem/add-atom
                   (chem/add-atom
                    (chem/make-molecule)
                    c1)
                   h1)
                  h2)
                 h3)
                h4)
               c1 h1)
              c1 h2)
             c1 h3)
            c1 h4)))
    #'user/ethane

This looks really tedious, but we'll see how to avoid this tedium
later. For the moment, let's explore some simple operations on ethane:

    (chem/mass ethane)
    ;=> 16.042461

    (chem/exact-mass ethane)
    ;=> 16.0313

    (map name (chem/atoms ethane))
    ;=> ("C1" "H2" "H3" "H1" "H4")

    (map (comp (partial map name) chem/atoms) (chem/bonds ethane))
    ;=> (("C1" "H4") ("C1" "H3") ("C1" "H2") ("C1" "H1"))

Ok, so it seems we do indeed have an object that represents ethane and
we can perform some simple operations on it. The last form is worthy
of examining more closely. Notice that this is as map form, that is
we'll be performing a function on each of the objects in the seq (the
clojure abstraction that provides sequential access to the items in
lists, vectors, maps, etc...) that we're mapping over, and
accumulating the results. The seq that we'll be mapping over is
(chem/bonds ethane), which, as one might expect, gives us a seq of the
bonds in the specified molecule. But just calling (chem/bonds ethane)
gives us the entire Bond object for each bond, more data than we want
for the moment:

    (chem/bonds ethane)
    ;=> (#:chemiclj.bond.Bond{:_nodes [#:chemiclj.atom.Atom{:_name "C1",
    :element #:chemiclj.element.Element{:atomic-number 6, :id "C", :name
    "carbon", :group 14, :period 2, :mass 12.0107, :electronegativity
    2.55, :max-bond-order 4}, :isotope nil, :chirality nil, :charge 0,
    :hybridization nil, :aromatic nil, :explicit-hydrogen-count nil}
    #:chemiclj.atom.Atom{:_name "H4", :element
    #:chemiclj.element.Element{:atomic-number 1, :id "H", :name
    "hydrogen", :group 1, :period 1, :mass 1.00794, :electronegativity
    2.1, :max-bond-order 1}, :isotope nil, :chirality nil, :charge 0,
    :hybridization nil, :aromatic nil, :explicit-hydrogen-count nil}],
    :type nil, :order nil, :direction nil} ...)

I've trimmed the output for brevity's sake, but this is more than
we want at the moment. We just want the names of the atoms in the
bonds. So, now we're going to map over the bonds, extracting the
names as we go. First we need the atoms, which we can get with
(chem/atoms <bond>), so we can try:

    (map chem/atoms (chem/bonds ethane))

    ;=> ([#:chemiclj.atom.Atom{:_name "C1", :element
    #:chemiclj.element.Element{:atomic-number 6, :id "C", :name "carbon",
    :group 14, :period 2, :mass 12.0107, :electronegativity 2.55,
    :max-bond-order 4}, :isotope nil, :chirality nil, :charge 0,
    :hybridization nil, :aromatic nil, :explicit-hydrogen-count nil}
    ... }

But this is just as bad as before. We need the name of the
atoms. But we can't just call name on the atoms, as what we've
gotten back from the map form is a seq of seqs, rather than just a
seq. We could do:

   (map #(map name %) (map chem/atoms (chem/bonds ethane)))

But I don't like the triple map above. It's logical that we'll have
two levels of mapping, because we have a seq of seqs, but we should be
able to get away with mapping a single function, which in turns maps
over its items and does the right thing. Two tricks we can use are
comp and partial. comp composes two functions, that is (comp f g)
returns a new function that does: (fn [...] (f (g ...))). Using comp,
we can map a single function that is the composition a function that
maps over the atoms, giving the names of the atoms, and the function
that gives us the atoms:

    (map
     (comp #(map name %) chem/atoms)
     (chem/bonds ethane))
    ;=> (("C1" "H4") ("C1" "H3") ("C1" "H2") ("C1" "H1"))

But now we get rid of the ugly #(map name %) form by partially applying
name to map, yielding a function that will take on argument and call (map
name <the arg>) on that argument:

    (map
     (comp (partial map name) chem/atoms)
     (chem/bonds ethane))
    (("C1" "H4") ("C1" "H3") ("C1" "H2") ("C1" "H1"))

So, there you have it. A long, complicated way to perform simple
operations on one of the simplest organic molecules. In the next
post we'll see how to avoid some of this tedium and start building
more complex molecules, exploring more of the chemiclj API.

--


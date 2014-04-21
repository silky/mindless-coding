mindless-coding
===============

Mindless, verified (erasably) coding using dependent types


redblack.v is a demonstration of Erasability in Coq.  This
demonstration generates verified code for Red/Black tree insert, find,
delete minimum (delmin) and delete functions, where all proof-related
aspects of the code have been erased.  The current state of the code
is that the keys are nats - but this should be easy to genericize
without much impact.  The files redblack.mli and redblack.ml were
generated by Coq's Extraction mechanism (the last line in redblack.v).

The Red/Black trees and functions used in the demonstrate feature very
elaborate specifications that attempt to formalize all
non-performance-related constraints.

- Why Coq, why not Agda or Idris?  Coq's Prop universe is almost a
  fully functional erasability mechanism as is - it just needs a
  single injectivity axiom on a single Prop (Erasable) to be fully
  functional.  As far as I can tell, something similar isn't possible
  with Agda's irrelevance notations because they already incorporate
  proof irrelevance (whereas in Coq, proof irrelevance is an
  additional axiom that isn't - and can't be - used here).  Idris is
  still experiencing growing pains at this point in time, but may
  become the most hospitable environment for erasability in the future
  (a built-in erasability mechanism is being developed for it).

- Functions are implemented in Coq using tactics in proof mode for
  three reasons: to benefit from the interactive-ness of proof mode,
  to enable the usage of tactics, and to avoid the complexity behind
  successfully using the match-with construct in Coq in complex
  dependently-typed-with-indices contexts.

- Why explicit erasability?  Why not allow the compiler to do it all
  for you?  This is an on-going debate.  Note that there is nothing
  about this demonstration that requires that the compiler not find
  more to erase, and erase it.  The opinion of the author is that
  having erasability work as a type constraint during implementation
  of functions helps to prevent the programmer from "cheating" by
  accidentally raiding should-be-erased code and using any information
  obtained in run-time (unerased) code, thus destroying the
  erasable-ness of the former.  It has a similar effect on tactics -
  they can't cheat either, so a more liberal usage of tactics is not
  discouraged.  One point of the demonstration here is that explicit
  erasability doesn't imply messy development - for example, it
  doesn't require re-implementation of any existing types or
  functions.

- Why a Red/Black tree?  It's well known, useful, and difficult to get
  right.  Hence, the ability here to "mindlessly" implement the
  insert, find, delmin, and especially the delete function for
  Red/Black trees with full erasability of all proof-related
  paraphernalia is a non-trivial accomplishment.  By "mindless", we
  refer to the nature of implementing these functions once their type
  specifications, as well as that of rbtree itself, are made
  sufficiently complete so as to constrain any implementation that
  type-checks to be fully correct.  The author did not use existing
  implementations of Red/Black trees for reference.

- What's the goal?  Explore the potential of "mindless" programming,
  as described above.  Erasability is important because it liberates
  specification from the concerns of burdening executable code with
  proof-related paraphernalia.  That's important because highly
  constraining specifications, in the form of very proof-laden
  dependent types, are needed guide the implementation to the point
  where the function implementer can just be concerned with satisfying
  small incremental goals, (mostly) without carrying around the
  cognitive load of the algorithm's details.

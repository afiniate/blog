---
layout: post
title: SML/MLton vs OCaml for Erlang Integration
---

{{ page.title }}
================

Over the last few days I have gotten virtually the same question
multiple times from a few different sources. So I thought I would
answer the question in a more complete way than a quick response. The
question is essentially why use
[SML (explicitly via MLton)](http://mlton.org) instead of
[OCaml](http://http://caml.inria.fr)

There are a few big reasons that We chose SML and very specifically the
MLton compiler. These reasons can be summed up as follows:

* Easy integration into an Erlang oriented build system where multiple
  languages may be in use.
* A threading system that is easily managed by Erlang.
* The ability to change the system for my use case.

Easy Integration Into The Build
-------------------------------

MLton, by design, will put out any number of intermediate build
results (archive files, shared objects, executables, etc). This makes
it very easy to integrate into a build system that is not SML/MLton
focused. Granted this is *possible* to do with OCaml, but it's much more
of a hack than anything else. It also seems to be unsupported by the
maintainers. I suspect the main deal here is that OCaml expects to be
driving the build while SML/MLton does not.

Managing Native Threads
-----------------------

Another major negative for OCaml is the existence of the GIL, or global
interpreter lock. OCaml allows for the creation of native threads but
any time the system enters any part of the 'core library' the entire
system is locked. Obviously, putting a big lock around the entire
library is something of a hack. It's a simple way for the OCaml
maintainers to give the semblance of multi-threading without the
reality.

MLton takes a much more interesting approach (from the perspective of
Erlang integration). It allows the user to create green threads via
CML, it then multiplexes those green threads using its own fairly
a simple scheduler. Not only is this a much more elegant approach (I
think), but because the thread that 'houses' the MLton runtime is
created outside of MLton itself, it makes it much easier for Erlang to
have more fine grained control over actual native threads consumed and
used. Of course, if you want to take advantage of multiple CPUs this
presents something of a problem; however, it's a problem that can be
overcome by simply loading multiple instances of the MLton runtime,
pinning their threads to the correct CPU and dispatching work
according to load from Erlang.

Changing The System
-------------------

MLton is also a much simpler system then OCaml. I am reasonably
confident that I can go in and change, say the garbage collector, or
add a special optimization pass to MLton if I need to. I don't expect
to have that requirement, but it's there if I need it. I realize my use
case is quite a bit different then the normal use case for MLton, so
that is a pretty important consideration. With OCaml I am much less
confident that I could do the same thing. At least not until I have
spent many months getting my mind around things.

Finally, one of big wins for OCaml is the size of its library. For
Erlang integration, where Erlang will be doing most of the heavy
lifting, that just isn't as compelling is it is in other situations.

A Final Note About Haskell
--------------------------

Haskell is an interesting language and it has some of the same
benefits as SML compiled via MLton. For example, it integrates well
with external build systems and has a well thought out threading
system (though it doesn't lend itself to external
management). However, the goal an external language is as an
optimization language. I have a very nice, well thought out functional
language in Erlang that I am using for the vast majority of the
system. For an optimization language I want something that will allow
*mostly* safe operations, but allows me to do deep and dirty things like mutation,
while retaining some of the safety a well typed, well thought out
functional language has. I do not believe that Haskell fits this bill as
well as SML does.


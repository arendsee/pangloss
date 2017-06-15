# Pangloss

Here I ramble about the language I wish I had. I don't know when, if ever,
I will start writing it.

# Ramble

Frustrated with the tedium of all other languages, I've decided to write
(another) new one, which will (like the other new ones) be the best of all
possible languages. The core principle of Pangloss is that testing, profiling
and documenting are all evil. If a program compiles, it is correct and
performant and the purpose is implicit in the type.

My two favorite languages are C (where what the code does is clear) and Haskell
(where what you want it to do is clear).

In C I know how memory is being used. I can step through my program mentally.
It is easy to write performant code and easy to be sure it is performant. But
as the code grows, as hacks are built on hacks, I have little assurance that
the program is correct. I have to rely on extensive external testing and
runtime checks. The code, though easy to understand, becomes repetitive in the
absence good polymorphism.

In Haskell, I know the type of every function and know, at the type level,
exactly what it does. I can look at the code and transform the types in my
head, I can prove that it will work. Of course I don't have to prove it, the
typechecker does that for me. However, performance is very hard to reason
about. I would have to master a great many tedius details to be able to predict
run-time performance. The greater the complexity of the compiler, the looser
the link between the human and machine code (well, vise vera is more true).

I want both. I want a language that is type-correct if it compiles, where every
function is total. But I also want to be able to reason exactly about the
memory usage and performance. More so, I want the compiler to reason about the
programs performance for me. I want to make declarations about the performance.

The language must be very simple. Complexity comes from the arrangement of
parts, not from additional features. Performance in time and space are part of
the type signature (though optional, since they can be inferred). All data
structures come directly from category theory. The laws they follow are
integrated into the type signatures (which may require dependent types).
Parallelism comes from exact, compile-time knowledge about the dependencies
between pieces. As in any functional language, data are immutable. The
dependencies are also be part of the signature (and also inferred).

Everything has properties. The compiler can infer these properties. And the
programmer can specify them in the signatures. The specifications should not be
required, but are checked. They take the place of benchmarking and most
testing.

And I don't just mean big-O complexity. We can infer much more than that. Let's
say you have a binary operator, '+'. The time requirement for running it is
`t(x,y)` where `x` and `y` are the arguments. There are terminal operators, the
lowest level functions all other functions are built on. The absolute time
required to run the program is defined in terms of them. Thus you should be
able to predict how much a particular change in hardware would affect program
performance. You can build equations for performance. On how the performance
will vary with input. These performance functions will parameterized with the
variables that can be set by the compiler. So the effect of variables or other
changes on performance becomes a statically calculable thing. Now, for this to
be true, there will have to be some limitations on the code. Everything will
have to terminate. Be guaranteed to terminate. This is a hard thing to do.

Type signatures are optional. If you don't particularly care about the
performance, you can leave this out of the type signature (it will be inferred
anyway). With more advanced type signatures, we can use it to refine how the
program works. These refinements alter performance and allow more properties to
be checked. But we start getting into architecture specific details. Though,
this is how the language ought to be. Entry is easy, don't specificy anything.
But additional layers of constraints can be added. These layers can be tucked
away, leaving pure simplicity behind. Advanced features don't change the code,
they wrap it. Such that in an editor, these layers can be made invisible.
A program can be written entirely in a very simple language. Then, without
changing it, additional layers can be added to refine the type. All the way
down to assembly, if you wish.

For a function to be total, say (x:Int + y:Int), every possible value must be
accounted for. If `Int` is any integer, the function must be complete across
negative to positive infinity. Partial functions will result in compile-time
errors.

All of this would require the code to potentially be a bit complicated. But the
simplicity of other language (for example Python) is a false simplicity. These
other languages require extensive use of testing, benchmarking, documentation,
specification, etc. If the language is totally typed, and if performance is
exactly solved, then profiling is not needed. Only minimal testing is needed.
You can declare that the program should be able to handle inputs of size x and
run on architecutre A. The program can generate sample input data that runs in
a reasonable time.

I will start the language by specifying the data types. These will come from
category theory. I will stay closer to mathematical ways of decribing things
than Haskell. Pangloss should be able to exactly describe a type like `ring`:
a set closed upon two associative, commutative, invertible operators where one
is distributive across the other. Now reality has to be accounted for here
(unlike in mathematics) since infinite sets are not always realistic. So
a given set is total only within the intersection between the set and the
Shadow. Where the Shadow is a complicated thing, dependent on the state of the
system. For example, a list may be defined as an appendable set with a zero
element. Lists can be combined to arbitrary sizes but are subject to the
Shadow, the list cannot grow outside the space allowed by memory constraints.
The actual space, will be defined at runtime by the operating system, and is
dependent on the state of the machine. Sometimes the Shadow is simple, for
example the size of an Int64 is limited to `2^64`; so an int64 monoid would
allow multiplication up to this value, then fail outside. We should be able to
model the circumstances under which a type will leave the Shadow. That is, we
should be able to describe the space of valid inputs.

I am heavily emphasizing static analysis for statistically deterministic
programs. But, I suppose, there are also real-time programs that have no
defined endpoint. Say code for a database that is on and listening as long as
the server is active. How to handle daemons? The answer is to reason in terms
of equilibria. Every data structure has a temporal property. You would describe
the program in terms of fluxes. Borrow ideas from chemistry, from metabolic
pathway analysis. If the program leaves the shadow, the system fails. It should
be designed and compiled such that this is either unlikely or impossible.

You need a lot of data to parameterize the models. You need to know what is
Gaussian and what is Cauchy.

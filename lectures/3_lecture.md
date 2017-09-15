### Questions
  - should we need to be able to recreate the proof of `1/(nk^(d-1))`?
  - do we need to be able to recreate or work with the CUZZ algorithm explained
    in the lecture notes?
##Testing Concurrent Programs
  - since the thread scheduling can't be deterministically set in any particular
    run, the input alone can't determine whether or not you'll get a concurrency
related bug.
  - programs like CUZZ insert random `sleep()` into the program.
    - this lowers the priority of particular threads during program execution,
      and is a way of FUZZing multithreaded applications

  - *Depth*: the depth of a concurrency bug is the # of `ordering constraints`
    that a thread schedule has to satisfy to find the bug
    - here's an example of an ordering constraint. Say there is one thread that
      sets a variable `x = 'hello'` and another thread that references this
value `this.x.reverse()`. Since one thread is *constrained* by its dependence on
`x`, the # of ordering constraints is 1

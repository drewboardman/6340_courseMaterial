| | Dynamic | Static |
| - | - | - |
| Cost  | Proportional to programs **execution time**  | Proportional to program's **size** |
| Effectiveness  | Unsound (may miss errors)  | Incomplete (may report spurious errors) |

## What is Program Analysis
  - PA can be generalized into three categories

### Dynamic Analysis (Run Time)
  - infers facts about a program by monitoring its runs
  - `Purify` is a tool for checking array bounds in C and C++ programs
  - `Valgrind` detects memory leaks in X86 binary programs
    - a memory leak is when a program fails to release memory that it isn't
      using anymore
  - `Eraser` detects race conditions in concurrent programs
    - this is when two threads in a concurrent program attempt to access the
      same memory location at the same time (same damn time) - where at least
one of those threads is *writing* to that memory location
    - obviously race conditions are a run time problem, since each run can
      produce different results depending on which thread 'wins'
  - `Daikon` finds likely invariants.
    - Invariants are program facts that is true in every run of the program

### Static Analysis (Compile Time)
  - Linters count as static analysis tools
  - `Microsoft SLAM` checks API usage rules. I think this is like contract testing
    (similar to Pacts) but for native software
    - They check whether device drivers use the Windows API correctly.
  - `Facebook INFER` checks for memory leaks in Android Apps
  - `ESC/Java` finds invariants in Java programs

### Hybrid Analysis (combines both)
  - There were no notes on this specifically in the lecture

### Discovering Invariants via Dynamic Analysis
  - So you'd use a tool like `Daikon` to attempt to find likely invariants
  - `Daikon` can't test an unbounded number of application runs, so *at best* it
    can make the claim that `c == 42` is a likey invariant
  - Can rule out *definitely variant values*. So Daikon can rule out large sets
    of input values as not invariant

### Discovering Invariants via Static Analysis
  - since static analysis tools can inspect source code, they can *definitely
    state* that `z == 42` is an invariant value

------------

## Terminology
  - Static analysis usually operates on a suitable intermediate representation
    of the program
    - an example of this is a *control flow graph*
  - The SA tool will track an abstract state at each step of the program
    - for instance, the three variable `x y z` will have values that can be
      tracked at each point in a particular run
  - Pro: has *Soundness* - whenever an SA tool determines that a variable has a
    constant value, it is definitely correct in *all runs* of the program
  - Con: lacks *Completeness* - an SA tool may fail to determine the abstract
    value of a particular variable over an unbounded possible execution chain
(maybe misunderstanding this here)

##### Abstract vs Concrete states
  - abstract state is tracking the values of each of the three variables at each
    program point
  - a concrete state is tracking the actual values in a particular run
  - SA doesn't run the program, so it doesn't operate over concrete states
  - each abstract state summarizes a *set* of concrete states

-----------

## Who needs Program Analysis?
  - I didn't add #2 and #3. They are Software Quality Tools and IDEs. I feel
    like it's obvious why those would want analysis tools

### 1 Compilers

  - use PA to generate efficient code
    - for instance, if a compiler uses SA to determine that two different loop
      branches produce the same value - it can eliminate parts of the code to
make the compiled code simpler

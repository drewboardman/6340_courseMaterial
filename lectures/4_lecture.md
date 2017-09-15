### Questions
  - so is Korat a property-based testing framework?

---------

# Lecture 4: Automated Test Generation

### Korat
  - testing framework
  - uses preconditions and postconditions to generate tests automatically
  - the **Small Test Case Hypothesis**
    - definition: *if there is a test that causes the program to fail, there is a small such test*
    - sounds similar to minimization
  - Korat uses *shapes* to represent test iterations
  - a shape is made by an arrangement of vectors

#### Example: General Case for Binary Trees

  - **REMEMBER**: This is the *general* solution (without any restrictions). When you actually take into account the rules of a valid tree, there are only 9 possible trees for `k == 3`

  - Question: How many binary trees are there of `size <= k` (where `k == number of nodes`)?
  - Calculation:
    - For a `BinaryTree` object `bt`
    - and `k` number of `Node` objects, `n0, n1, n2, ...`
    - each `Node` has 2 possible pointers, and the original pointer to the root node
      - this means there are `2k + 1` pointers
    - each pointer can have `null` or another `Node` as its value
      - this means there are `1 + k` possible values for pointers
    - therefor there are `(1 + k)^(2k + 1)` possible configurations

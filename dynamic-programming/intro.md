# Dynamic Programming

Dynamic Programming (DP) is a powerful algorithmic paradigm that solves complex problems by **breaking them down into simpler subproblems** and **storing the results** to avoid redundant calculations. The key insight is to identify overlapping subproblems and optimal substructure, then solve each subproblem only once.

## When to Use Dynamic Programming

Dynamic Programming is ideal for problems that exhibit:

- **Optimal substructure**: The optimal solution contains optimal solutions to subproblems.
- **Overlapping subproblems**: The same subproblems are solved multiple times in a naive approach.
- **Sequential decision making**: Where decisions depend on previous choices.
- **Counting problems**: Finding the number of ways to do something.

## Why Use Dynamic Programming?

- **Efficiency**: Reduces exponential time complexity to polynomial by avoiding redundant calculations.
- **Optimal solutions**: Guarantees optimal solutions for problems with optimal substructure.
- **Memory vs. time trade-off**: Uses extra space to significantly reduce time complexity.
- **Systematic approach**: Provides a structured way to think about complex problems.

## Common Use Cases

1. **Fibonacci sequence**: Classic example of overlapping subproblems.
2. **Knapsack problems**: Optimizing resource allocation with constraints.
3. **Longest common subsequence**: Finding patterns in sequences.
4. **Path counting**: Counting unique paths in grids or graphs.
5. **String problems**: Edit distance, palindromes, pattern matching. 
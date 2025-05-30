# Backtracking

Backtracking is a systematic method for solving constraint satisfaction problems by **incrementally building candidates** to the solutions and **abandoning candidates** ("backtracking") when they cannot possibly be extended to a valid solution. It's essentially a refined brute force approach that prunes the search space early.

## When to Use Backtracking

Backtracking is ideal for problems where you need to:

- **Generate all possible combinations or permutations**: Such as generating all subsets, permutations, or combinations.
- **Find all valid solutions**: Like solving puzzles (N-Queens, Sudoku) or finding all paths in a maze.
- **Constraint satisfaction**: Problems where you need to satisfy multiple constraints simultaneously.
- **Decision problems**: Where you make a series of choices and need to explore all possibilities.

## Why Use Backtracking?

- **Systematic exploration**: Explores all possible solutions in a structured manner.
- **Early pruning**: Abandons invalid paths early, saving computation time.
- **Memory efficient**: Uses recursion stack, avoiding explicit storage of all partial solutions.
- **Versatile**: Applicable to a wide range of combinatorial and constraint satisfaction problems.

## Common Use Cases

1. **Combinatorial Problems**: Generating subsets, permutations, combinations.
2. **Puzzles**: N-Queens, Sudoku, word search in a grid.
3. **Path Finding**: Finding all paths in a graph or maze.
4. **Constraint Satisfaction**: Problems with multiple constraints that must be satisfied simultaneously. 
# Breadth-First Search (BFS)

Breadth-First Search (BFS) is a fundamental graph traversal algorithm that explores all nodes at the **current depth level** before moving to nodes at the next depth level. It systematically visits nodes **level by level**, making it particularly useful for finding **shortest paths**, **level-order traversals**, and **minimum steps** problems.

## When to Use BFS

BFS is ideal for problems where you need to:

- **Find shortest paths**: In unweighted graphs or grids where each step has equal cost.
- **Level-order traversal**: Exploring trees or graphs level by level.
- **Minimum steps problems**: Finding the minimum number of operations to reach a target.
- **Connected components**: Finding all nodes reachable from a starting point.
- **Shortest transformation**: Finding minimum steps to transform one state to another.

## Why Use BFS?

- **Optimal for shortest paths**: Guarantees shortest path in unweighted graphs.
- **Level-by-level exploration**: Perfect for problems requiring level-order processing.
- **Complete search**: Explores all possibilities at each level before going deeper.
- **Memory vs. depth trade-off**: Uses more memory than DFS but finds solutions faster for shortest path problems.

## Common Use Cases

1. **Tree Level Order**: Traversing binary trees level by level.
2. **Shortest Path**: Finding shortest path in unweighted graphs or grids.
3. **Word Ladder**: Minimum transformations between words.
4. **Minimum Steps**: Finding minimum moves in puzzle games.
5. **Network Analysis**: Finding closest connections in social networks. 
# Depth-First Search (DFS)

Depth-First Search (DFS) is a fundamental graph traversal algorithm that explores as far as possible along each branch before **backtracking**. It systematically visits nodes by going deeper into the graph structure before exploring neighbors, making it particularly useful for problems involving **path finding**, **connectivity**, and **topological ordering**.

## When to Use DFS

DFS is ideal for problems where you need to:

- **Explore all paths**: Such as finding all paths from source to destination in a graph.
- **Detect cycles**: Identifying circular dependencies in directed or undirected graphs.
- **Topological sorting**: Ordering vertices in a directed acyclic graph based on dependencies.
- **Connected components**: Finding all connected components in a graph.
- **Tree traversals**: In-order, pre-order, and post-order traversals of binary trees.

## Why Use DFS?

- **Memory efficient**: Uses stack space proportional to the depth of the graph, often less than BFS.
- **Simple implementation**: Can be implemented elegantly using recursion or explicit stack.
- **Path reconstruction**: Easy to track and reconstruct paths during traversal.
- **Early termination**: Can stop as soon as a solution is found in many cases.

## Common Use Cases

1. **Tree Traversals**: Pre-order, in-order, post-order traversals of binary trees.
2. **Path Finding**: Finding any path between two nodes in a graph.
3. **Cycle Detection**: Detecting cycles in both directed and undirected graphs.
4. **Maze Solving**: Finding paths through mazes using recursive backtracking.
5. **Topological Sort**: Ordering tasks with dependencies using DFS post-order. 
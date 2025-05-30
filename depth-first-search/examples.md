# Examples

## Maximum Depth of Binary Tree
?> LeetCode: [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/) `Easy`

- **Simplified Problem**: Given the root of a binary tree, return its maximum depth. The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

- **Solution Approach**: Use DFS recursively. The depth of a tree is 1 plus the maximum depth of its left and right subtrees.

```pseudocode
dfs(node):
    if node is null:
        return 0
    return 1 + max(dfs(node.left), dfs(node.right))
```

<!-- tabs:start -->
### **Go**
```go
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func maxDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    return 1 + max(maxDepth(root.Left), maxDepth(root.Right))
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

### **Python**
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def maxDepth(root):
    if not root:
        return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))
```
<!-- tabs:end -->

---

## Number of Islands
?> LeetCode: [200. Number of Islands](https://leetcode.com/problems/number-of-islands/description/) `Medium`

- **Simplified Problem**: Given an m x n 2D binary grid which represents a map of '1's (land) and '0's (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

- **Solution Approach**: Use DFS to explore each island. When we find a '1', increment the count and use DFS to mark all connected land cells as visited.

<!-- tabs:start -->
### **Go**
```go
func numIslands(grid [][]byte) int {
    if len(grid) == 0 || len(grid[0]) == 0 {
        return 0
    }
    
    rows, cols := len(grid), len(grid[0])
    count := 0
    
    var dfs func(int, int)
    dfs = func(r, c int) {
        if r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] == '0' {
            return
        }
        
        grid[r][c] = '0' // Mark as visited
        
        // Explore all 4 directions
        dfs(r+1, c)
        dfs(r-1, c)
        dfs(r, c+1)
        dfs(r, c-1)
    }
    
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if grid[i][j] == '1' {
                count++
                dfs(i, j)
            }
        }
    }
    
    return count
}
```

### **Python**
```python
def numIslands(grid):
    if not grid or not grid[0]:
        return 0
    
    rows, cols = len(grid), len(grid[0])
    count = 0
    
    def dfs(r, c):
        if (r < 0 or r >= rows or c < 0 or c >= cols or 
            grid[r][c] == '0'):
            return
        
        grid[r][c] = '0'  # Mark as visited
        
        # Explore all 4 directions
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)
    
    for i in range(rows):
        for j in range(cols):
            if grid[i][j] == '1':
                count += 1
                dfs(i, j)
    
    return count
```
<!-- tabs:end -->

---

## Path Sum
?> LeetCode: [112. Path Sum](https://leetcode.com/problems/path-sum/description/) `Easy`

- **Simplified Problem**: Given the root of a binary tree and an integer targetSum, return true if the tree has a root-to-leaf path such that adding up all the values along the path equals targetSum.

- **Solution Approach**: Use DFS to traverse all root-to-leaf paths. At each node, subtract its value from the target sum and check if we reach a leaf with sum equal to the node's value.

<!-- tabs:start -->
### **Go**
```go
func hasPathSum(root *TreeNode, targetSum int) bool {
    if root == nil {
        return false
    }
    
    // If it's a leaf node, check if the remaining sum equals node value
    if root.Left == nil && root.Right == nil {
        return targetSum == root.Val
    }
    
    // Recursively check left and right subtrees with reduced sum
    return hasPathSum(root.Left, targetSum-root.Val) || 
           hasPathSum(root.Right, targetSum-root.Val)
}
```

### **Python**
```python
def hasPathSum(root, targetSum):
    if not root:
        return False
    
    # If it's a leaf node, check if remaining sum equals node value
    if not root.left and not root.right:
        return targetSum == root.val
    
    # Recursively check left and right subtrees with reduced sum
    return (hasPathSum(root.left, targetSum - root.val) or
            hasPathSum(root.right, targetSum - root.val))
```
<!-- tabs:end -->

---

## Course Schedule
?> LeetCode: [207. Course Schedule](https://leetcode.com/problems/course-schedule/description/) `Medium`

- **Simplified Problem**: Given the total number of courses and a list of prerequisite pairs, determine if you can finish all courses. This is essentially a cycle detection problem in a directed graph.

- **Solution Approach**: Use DFS to detect cycles in the course dependency graph. Use three states: unvisited (0), visiting (1), and visited (2). If we encounter a node in the visiting state, we've found a cycle.

<!-- tabs:start -->
### **Go**
```go
func canFinish(numCourses int, prerequisites [][]int) bool {
    // Build adjacency list
    graph := make([][]int, numCourses)
    for _, prereq := range prerequisites {
        course, pre := prereq[0], prereq[1]
        graph[pre] = append(graph[pre], course)
    }
    
    // 0: unvisited, 1: visiting, 2: visited
    state := make([]int, numCourses)
    
    var dfs func(int) bool
    dfs = func(course int) bool {
        if state[course] == 1 { // Cycle detected
            return false
        }
        if state[course] == 2 { // Already processed
            return true
        }
        
        state[course] = 1 // Mark as visiting
        
        for _, neighbor := range graph[course] {
            if !dfs(neighbor) {
                return false
            }
        }
        
        state[course] = 2 // Mark as visited
        return true
    }
    
    for i := 0; i < numCourses; i++ {
        if !dfs(i) {
            return false
        }
    }
    
    return true
}
```

### **Python**
```python
def canFinish(numCourses, prerequisites):
    # Build adjacency list
    graph = [[] for _ in range(numCourses)]
    for course, pre in prerequisites:
        graph[pre].append(course)
    
    # 0: unvisited, 1: visiting, 2: visited
    state = [0] * numCourses
    
    def dfs(course):
        if state[course] == 1:  # Cycle detected
            return False
        if state[course] == 2:  # Already processed
            return True
        
        state[course] = 1  # Mark as visiting
        
        for neighbor in graph[course]:
            if not dfs(neighbor):
                return False
        
        state[course] = 2  # Mark as visited
        return True
    
    for i in range(numCourses):
        if not dfs(i):
            return False
    
    return True
```
<!-- tabs:end --> 
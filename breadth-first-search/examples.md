# Examples

## Binary Tree Level Order Traversal
?> LeetCode: [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/) `Medium`

- **Simplified Problem**: Given the root of a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

- **Solution Approach**: Use BFS with a queue to process nodes level by level. Keep track of the number of nodes at each level to group them correctly.

```pseudocode
bfs(root):
    if root is null: return empty
    queue = [root]
    result = []
    while queue is not empty:
        level_size = queue.size()
        current_level = []
        for i from 0 to level_size:
            node = queue.dequeue()
            current_level.add(node.val)
            if node.left: queue.enqueue(node.left)
            if node.right: queue.enqueue(node.right)
        result.add(current_level)
    return result
```

<!-- tabs:start -->
### **Go**
```go
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func levelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{}
    }
    
    result := [][]int{}
    queue := []*TreeNode{root}
    
    for len(queue) > 0 {
        levelSize := len(queue)
        currentLevel := []int{}
        
        for i := 0; i < levelSize; i++ {
            node := queue[0]
            queue = queue[1:]
            currentLevel = append(currentLevel, node.Val)
            
            if node.Left != nil {
                queue = append(queue, node.Left)
            }
            if node.Right != nil {
                queue = append(queue, node.Right)
            }
        }
        
        result = append(result, currentLevel)
    }
    
    return result
}
```

### **Python**
```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def levelOrder(root):
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        current_level = []
        
        for _ in range(level_size):
            node = queue.popleft()
            current_level.append(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(current_level)
    
    return result
```
<!-- tabs:end -->

---

## Minimum Depth of Binary Tree
?> LeetCode: [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/) `Easy`

- **Simplified Problem**: Given a binary tree, find its minimum depth. The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

- **Solution Approach**: Use BFS to find the first leaf node encountered, which guarantees the minimum depth due to level-by-level exploration.

<!-- tabs:start -->
### **Go**
```go
func minDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    
    queue := []*TreeNode{root}
    depth := 1
    
    for len(queue) > 0 {
        levelSize := len(queue)
        
        for i := 0; i < levelSize; i++ {
            node := queue[0]
            queue = queue[1:]
            
            // Check if it's a leaf node
            if node.Left == nil && node.Right == nil {
                return depth
            }
            
            if node.Left != nil {
                queue = append(queue, node.Left)
            }
            if node.Right != nil {
                queue = append(queue, node.Right)
            }
        }
        
        depth++
    }
    
    return depth
}
```

### **Python**
```python
from collections import deque

def minDepth(root):
    if not root:
        return 0
    
    queue = deque([root])
    depth = 1
    
    while queue:
        level_size = len(queue)
        
        for _ in range(level_size):
            node = queue.popleft()
            
            # Check if it's a leaf node
            if not node.left and not node.right:
                return depth
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        depth += 1
    
    return depth
```
<!-- tabs:end -->

---

## Word Ladder
?> LeetCode: [127. Word Ladder](https://leetcode.com/problems/word-ladder/description/) `Hard`

- **Simplified Problem**: Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord. Each transformation can only change one letter at a time.

- **Solution Approach**: Use BFS to find the shortest transformation path. Treat each word as a node and each valid transformation as an edge in a graph.

<!-- tabs:start -->
### **Go**
```go
func ladderLength(beginWord string, endWord string, wordList []string) int {
    wordSet := make(map[string]bool)
    for _, word := range wordList {
        wordSet[word] = true
    }
    
    if !wordSet[endWord] {
        return 0
    }
    
    queue := []string{beginWord}
    visited := make(map[string]bool)
    visited[beginWord] = true
    level := 1
    
    for len(queue) > 0 {
        levelSize := len(queue)
        
        for i := 0; i < levelSize; i++ {
            word := queue[0]
            queue = queue[1:]
            
            if word == endWord {
                return level
            }
            
            // Try changing each character
            for j := 0; j < len(word); j++ {
                for c := 'a'; c <= 'z'; c++ {
                    if c == rune(word[j]) {
                        continue
                    }
                    
                    newWord := word[:j] + string(c) + word[j+1:]
                    if wordSet[newWord] && !visited[newWord] {
                        visited[newWord] = true
                        queue = append(queue, newWord)
                    }
                }
            }
        }
        
        level++
    }
    
    return 0
}
```

### **Python**
```python
from collections import deque

def ladderLength(beginWord, endWord, wordList):
    word_set = set(wordList)
    if endWord not in word_set:
        return 0
    
    queue = deque([beginWord])
    visited = {beginWord}
    level = 1
    
    while queue:
        level_size = len(queue)
        
        for _ in range(level_size):
            word = queue.popleft()
            
            if word == endWord:
                return level
            
            # Try changing each character
            for i in range(len(word)):
                for c in 'abcdefghijklmnopqrstuvwxyz':
                    if c == word[i]:
                        continue
                    
                    new_word = word[:i] + c + word[i+1:]
                    if new_word in word_set and new_word not in visited:
                        visited.add(new_word)
                        queue.append(new_word)
        
        level += 1
    
    return 0
```
<!-- tabs:end -->

---

## Rotting Oranges
?> LeetCode: [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/description/) `Medium`

- **Simplified Problem**: Given a grid where 0 = empty, 1 = fresh orange, 2 = rotten orange. Every minute, rotten oranges cause adjacent fresh oranges to rot. Return the minimum time until no fresh oranges remain, or -1 if impossible.

- **Solution Approach**: Use multi-source BFS starting from all initially rotten oranges simultaneously. Count the time levels until all fresh oranges are rotten.

<!-- tabs:start -->
### **Go**
```go
func orangesRotting(grid [][]int) int {
    rows, cols := len(grid), len(grid[0])
    queue := [][]int{}
    freshCount := 0
    
    // Find all rotten oranges and count fresh ones
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if grid[i][j] == 2 {
                queue = append(queue, []int{i, j})
            } else if grid[i][j] == 1 {
                freshCount++
            }
        }
    }
    
    if freshCount == 0 {
        return 0
    }
    
    directions := [][]int{{-1, 0}, {1, 0}, {0, -1}, {0, 1}}
    minutes := 0
    
    for len(queue) > 0 && freshCount > 0 {
        levelSize := len(queue)
        
        for i := 0; i < levelSize; i++ {
            curr := queue[0]
            queue = queue[1:]
            row, col := curr[0], curr[1]
            
            for _, dir := range directions {
                newRow, newCol := row+dir[0], col+dir[1]
                
                if newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols &&
                   grid[newRow][newCol] == 1 {
                    grid[newRow][newCol] = 2
                    freshCount--
                    queue = append(queue, []int{newRow, newCol})
                }
            }
        }
        
        minutes++
    }
    
    if freshCount == 0 {
        return minutes
    }
    return -1
}
```

### **Python**
```python
from collections import deque

def orangesRotting(grid):
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh_count = 0
    
    # Find all rotten oranges and count fresh ones
    for i in range(rows):
        for j in range(cols):
            if grid[i][j] == 2:
                queue.append((i, j))
            elif grid[i][j] == 1:
                fresh_count += 1
    
    if fresh_count == 0:
        return 0
    
    directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    minutes = 0
    
    while queue and fresh_count > 0:
        level_size = len(queue)
        
        for _ in range(level_size):
            row, col = queue.popleft()
            
            for dr, dc in directions:
                new_row, new_col = row + dr, col + dc
                
                if (0 <= new_row < rows and 0 <= new_col < cols and
                    grid[new_row][new_col] == 1):
                    grid[new_row][new_col] = 2
                    fresh_count -= 1
                    queue.append((new_row, new_col))
        
        minutes += 1
    
    return minutes if fresh_count == 0 else -1
```
<!-- tabs:end --> 
# Examples

## Subsets
?> LeetCode: [78. Subsets](https://leetcode.com/problems/subsets/description/) `Medium`

- **Simplified Problem**: Given an integer array nums of unique elements, return all possible subsets (the power set). The solution set must not contain duplicate subsets.

- **Solution Approach**: Use backtracking to build subsets incrementally. For each element, we have two choices: include it in the current subset or exclude it. We explore both choices recursively and backtrack when we reach the base case.

```pseudocode
backtrack(current_subset, start_index):
    add current_subset to result
    for i from start_index to end:
        add nums[i] to current_subset
        backtrack(current_subset, i + 1)
        remove nums[i] from current_subset  // backtrack
```

<!-- tabs:start -->
### **Go**
```go
func subsets(nums []int) [][]int {
    result := [][]int{}
    current := []int{}
    backtrack(nums, 0, current, &result)
    return result
}

func backtrack(nums []int, start int, current []int, result *[][]int) {
    // Make a copy of current subset and add to result
    subset := make([]int, len(current))
    copy(subset, current)
    *result = append(*result, subset)
    
    // Try adding each remaining number
    for i := start; i < len(nums); i++ {
        current = append(current, nums[i])
        backtrack(nums, i+1, current, result)
        current = current[:len(current)-1] // backtrack
    }
}
```

### **Python**
```python
def subsets(nums):
    result = []
    
    def backtrack(current, start):
        result.append(current[:])  # Add copy of current subset
        
        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(current, i + 1)
            current.pop()  # backtrack
    
    backtrack([], 0)
    return result
```
<!-- tabs:end -->

---

## Generate Parentheses
?> LeetCode: [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/description/) `Medium`

- **Simplified Problem**: Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

- **Solution Approach**: Use backtracking with constraints. At each step, we can either add an opening parenthesis (if we haven't used all n) or a closing parenthesis (if it won't make the string invalid). We backtrack when we reach a complete valid combination.

<!-- tabs:start -->
### **Go**
```go
func generateParenthesis(n int) []string {
    result := []string{}
    backtrack("", 0, 0, n, &result)
    return result
}

func backtrack(current string, open, close, max int, result *[]string) {
    if len(current) == max*2 {
        *result = append(*result, current)
        return
    }
    
    if open < max {
        backtrack(current+"(", open+1, close, max, result)
    }
    if close < open {
        backtrack(current+")", open, close+1, max, result)
    }
}
```

### **Python**
```python
def generateParenthesis(n):
    result = []
    
    def backtrack(current, open_count, close_count):
        if len(current) == 2 * n:
            result.append(current)
            return
        
        if open_count < n:
            backtrack(current + "(", open_count + 1, close_count)
        if close_count < open_count:
            backtrack(current + ")", open_count, close_count + 1)
    
    backtrack("", 0, 0)
    return result
```
<!-- tabs:end -->

---

## Permutations
?> LeetCode: [46. Permutations](https://leetcode.com/problems/permutations/description/) `Medium`

- **Simplified Problem**: Given an array nums of distinct integers, return all possible permutations in any order.

- **Solution Approach**: Use backtracking to build permutations. At each step, try adding each unused number to the current permutation. When the permutation is complete, add it to the result and backtrack.

<!-- tabs:start -->
### **Go**
```go
func permute(nums []int) [][]int {
    result := [][]int{}
    used := make([]bool, len(nums))
    current := []int{}
    backtrack(nums, current, used, &result)
    return result
}

func backtrack(nums, current []int, used []bool, result *[][]int) {
    if len(current) == len(nums) {
        perm := make([]int, len(current))
        copy(perm, current)
        *result = append(*result, perm)
        return
    }
    
    for i := 0; i < len(nums); i++ {
        if !used[i] {
            used[i] = true
            current = append(current, nums[i])
            backtrack(nums, current, used, result)
            current = current[:len(current)-1] // backtrack
            used[i] = false
        }
    }
}
```

### **Python**
```python
def permute(nums):
    result = []
    
    def backtrack(current):
        if len(current) == len(nums):
            result.append(current[:])
            return
        
        for num in nums:
            if num not in current:
                current.append(num)
                backtrack(current)
                current.pop()  # backtrack
    
    backtrack([])
    return result
```
<!-- tabs:end -->

---

## Word Search
?> LeetCode: [79. Word Search](https://leetcode.com/problems/word-search/description/) `Medium`

- **Simplified Problem**: Given an m x n grid of characters board and a string word, return true if word exists in the grid. The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring.

- **Solution Approach**: Use backtracking with DFS. For each cell that matches the first character of the word, start a DFS search. Mark visited cells and backtrack by unmarking them when the path doesn't lead to a solution.

<!-- tabs:start -->
### **Go**
```go
func exist(board [][]byte, word string) bool {
    rows, cols := len(board), len(board[0])
    
    var backtrack func(int, int, int) bool
    backtrack = func(row, col, index int) bool {
        if index == len(word) {
            return true
        }
        
        if row < 0 || row >= rows || col < 0 || col >= cols || 
           board[row][col] != word[index] {
            return false
        }
        
        // Mark as visited
        temp := board[row][col]
        board[row][col] = '#'
        
        // Explore all 4 directions
        found := backtrack(row+1, col, index+1) ||
                backtrack(row-1, col, index+1) ||
                backtrack(row, col+1, index+1) ||
                backtrack(row, col-1, index+1)
        
        // Backtrack
        board[row][col] = temp
        return found
    }
    
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if backtrack(i, j, 0) {
                return true
            }
        }
    }
    return false
}
```

### **Python**
```python
def exist(board, word):
    rows, cols = len(board), len(board[0])
    
    def backtrack(row, col, index):
        if index == len(word):
            return True
        
        if (row < 0 or row >= rows or col < 0 or col >= cols or
            board[row][col] != word[index]):
            return False
        
        # Mark as visited
        temp = board[row][col]
        board[row][col] = '#'
        
        # Explore all 4 directions
        found = (backtrack(row + 1, col, index + 1) or
                backtrack(row - 1, col, index + 1) or
                backtrack(row, col + 1, index + 1) or
                backtrack(row, col - 1, index + 1))
        
        # Backtrack
        board[row][col] = temp
        return found
    
    for i in range(rows):
        for j in range(cols):
            if backtrack(i, j, 0):
                return True
    return False
```
<!-- tabs:end --> 
# Examples

## Climbing Stairs
?> LeetCode: [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/) `Easy`

- **Simplified Problem**: You're climbing a staircase with n steps. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

- **Solution Approach**: This is a classic DP problem similar to Fibonacci. The number of ways to reach step n is the sum of ways to reach step n-1 plus ways to reach step n-2.

```pseudocode
dp[i] = number of ways to reach step i
dp[i] = dp[i-1] + dp[i-2]
```

<!-- tabs:start -->
### **Go**
```go
func climbStairs(n int) int {
    if n <= 2 {
        return n
    }
    
    // Space optimized approach
    prev2, prev1 := 1, 2
    for i := 3; i <= n; i++ {
        current := prev1 + prev2
        prev2 = prev1
        prev1 = current
    }
    return prev1
}

// Alternative: Using DP array
func climbStairsDP(n int) int {
    if n <= 2 {
        return n
    }
    
    dp := make([]int, n+1)
    dp[1], dp[2] = 1, 2
    
    for i := 3; i <= n; i++ {
        dp[i] = dp[i-1] + dp[i-2]
    }
    
    return dp[n]
}
```

### **Python**
```python
def climbStairs(n):
    if n <= 2:
        return n
    
    # Space optimized approach
    prev2, prev1 = 1, 2
    for i in range(3, n + 1):
        current = prev1 + prev2
        prev2 = prev1
        prev1 = current
    
    return prev1

# Alternative: Using DP array
def climbStairsDP(n):
    if n <= 2:
        return n
    
    dp = [0] * (n + 1)
    dp[1], dp[2] = 1, 2
    
    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]
```
<!-- tabs:end -->

---

## House Robber
?> LeetCode: [198. House Robber](https://leetcode.com/problems/house-robber/description/) `Medium`

- **Simplified Problem**: You are a robber planning to rob houses along a street. Each house has a certain amount of money. Adjacent houses have security systems connected, so you cannot rob adjacent houses. What is the maximum amount you can rob?

- **Solution Approach**: For each house, decide whether to rob it or not. If we rob current house, we can't rob the previous one. The maximum is either rob current house + max from two houses back, or don't rob current house and take max from previous house.

<!-- tabs:start -->
### **Go**
```go
func rob(nums []int) int {
    if len(nums) == 0 {
        return 0
    }
    if len(nums) == 1 {
        return nums[0]
    }
    
    // Space optimized approach
    prev2, prev1 := 0, nums[0]
    
    for i := 1; i < len(nums); i++ {
        current := max(prev1, prev2+nums[i])
        prev2 = prev1
        prev1 = current
    }
    
    return prev1
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
def rob(nums):
    if not nums:
        return 0
    if len(nums) == 1:
        return nums[0]
    
    # Space optimized approach
    prev2, prev1 = 0, nums[0]
    
    for i in range(1, len(nums)):
        current = max(prev1, prev2 + nums[i])
        prev2 = prev1
        prev1 = current
    
    return prev1
```
<!-- tabs:end -->

---

## Longest Increasing Subsequence
?> LeetCode: [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/) `Medium`

- **Simplified Problem**: Given an integer array nums, return the length of the longest strictly increasing subsequence.

- **Solution Approach**: Use DP where dp[i] represents the length of the longest increasing subsequence ending at index i. For each element, check all previous elements and extend the longest subsequence that can be extended.

<!-- tabs:start -->
### **Go**
```go
func lengthOfLIS(nums []int) int {
    if len(nums) == 0 {
        return 0
    }
    
    dp := make([]int, len(nums))
    for i := range dp {
        dp[i] = 1 // Each element forms a subsequence of length 1
    }
    
    maxLength := 1
    
    for i := 1; i < len(nums); i++ {
        for j := 0; j < i; j++ {
            if nums[j] < nums[i] {
                dp[i] = max(dp[i], dp[j]+1)
            }
        }
        maxLength = max(maxLength, dp[i])
    }
    
    return maxLength
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
def lengthOfLIS(nums):
    if not nums:
        return 0
    
    dp = [1] * len(nums)  # Each element forms a subsequence of length 1
    
    for i in range(1, len(nums)):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    
    return max(dp)
```
<!-- tabs:end -->

---

## Coin Change
?> LeetCode: [322. Coin Change](https://leetcode.com/problems/coin-change/description/) `Medium`

- **Simplified Problem**: Given an array of coin denominations and a target amount, return the fewest number of coins needed to make up that amount. If it's impossible, return -1.

- **Solution Approach**: Use bottom-up DP. For each amount from 1 to target, try using each coin and take the minimum number of coins needed.

<!-- tabs:start -->
### **Go**
```go
func coinChange(coins []int, amount int) int {
    // dp[i] represents minimum coins needed for amount i
    dp := make([]int, amount+1)
    
    // Initialize with impossible value (amount + 1)
    for i := range dp {
        dp[i] = amount + 1
    }
    dp[0] = 0 // Base case: 0 coins needed for amount 0
    
    for i := 1; i <= amount; i++ {
        for _, coin := range coins {
            if coin <= i {
                dp[i] = min(dp[i], dp[i-coin]+1)
            }
        }
    }
    
    if dp[amount] > amount {
        return -1
    }
    return dp[amount]
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

### **Python**
```python
def coinChange(coins, amount):
    # dp[i] represents minimum coins needed for amount i
    dp = [amount + 1] * (amount + 1)
    dp[0] = 0  # Base case: 0 coins needed for amount 0
    
    for i in range(1, amount + 1):
        for coin in coins:
            if coin <= i:
                dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[amount] if dp[amount] <= amount else -1
```
<!-- tabs:end -->

---

## Unique Paths
?> LeetCode: [62. Unique Paths](https://leetcode.com/problems/unique-paths/description/) `Medium`

- **Simplified Problem**: A robot is located at the top-left corner of an m x n grid. The robot can only move either down or right. How many possible unique paths are there to reach the bottom-right corner?

- **Solution Approach**: Use DP where dp[i][j] represents the number of ways to reach cell (i,j). A cell can be reached from the cell above or the cell to the left.

<!-- tabs:start -->
### **Go**
```go
func uniquePaths(m int, n int) int {
    // Space optimized: only need previous row
    prev := make([]int, n)
    for j := 0; j < n; j++ {
        prev[j] = 1
    }
    
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            prev[j] += prev[j-1]
        }
    }
    
    return prev[n-1]
}

// Alternative: Using 2D DP array
func uniquePaths2D(m int, n int) int {
    dp := make([][]int, m)
    for i := range dp {
        dp[i] = make([]int, n)
    }
    
    // Initialize first row and column
    for i := 0; i < m; i++ {
        dp[i][0] = 1
    }
    for j := 0; j < n; j++ {
        dp[0][j] = 1
    }
    
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
        }
    }
    
    return dp[m-1][n-1]
}
```

### **Python**
```python
def uniquePaths(m, n):
    # Space optimized: only need previous row
    prev = [1] * n
    
    for i in range(1, m):
        for j in range(1, n):
            prev[j] += prev[j-1]
    
    return prev[n-1]

# Alternative: Using 2D DP array
def uniquePaths2D(m, n):
    dp = [[1] * n for _ in range(m)]
    
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    
    return dp[m-1][n-1]
```
<!-- tabs:end --> 
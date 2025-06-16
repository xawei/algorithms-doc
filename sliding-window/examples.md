# Examples

## Maximum Average Subarray I
?> LeetCode: [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/description/) `Easy`

- **Simplified Problem**: Given an integer array nums and an integer k, find a contiguous subarray whose length is equal to k that has the maximum average value and return this value.

- **Solution Approach**: Use a fixed-size sliding window. Calculate the sum of the first k elements, then slide the window by removing the leftmost element and adding the new rightmost element.

<!-- tabs:start -->
### **Go**
```go
func findMaxAverage(nums []int, k int) float64 {
    // Calculate sum of first window
    windowSum := 0
    for i := 0; i < k; i++ {
        windowSum += nums[i]
    }
    
    maxSum := windowSum
    
    // Slide the window
    for i := k; i < len(nums); i++ {
        windowSum = windowSum - nums[i-k] + nums[i]
        if windowSum > maxSum {
            maxSum = windowSum
        }
    }
    
    return float64(maxSum) / float64(k)
}
```

### **Python**
```python
def findMaxAverage(nums, k):
    # Calculate sum of first window
    window_sum = sum(nums[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, len(nums)):
        window_sum = window_sum - nums[i-k] + nums[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum / k
```
<!-- tabs:end -->

---

## Longest Substring Without Repeating Characters
?> LeetCode: [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/) `Medium`

- **Simplified Problem**: Given a string s, find the length of the longest substring without repeating characters.

- **Solution Approach**: Use a variable-size sliding window with a hash set to track characters. Expand the window by moving the right pointer, and contract by moving the left pointer when duplicates are found.

<!-- tabs:start -->
### **Go**
```go
func lengthOfLongestSubstring(s string) int {
    charSet := make(map[byte]bool)
    left := 0
    maxLength := 0
    
    for right := 0; right < len(s); right++ {
        // Contract window until no duplicates
        for charSet[s[right]] {
            delete(charSet, s[left])
            left++
        }
        
        // Add current character and update max length
        charSet[s[right]] = true
        maxLength = max(maxLength, right-left+1)
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
def lengthOfLongestSubstring(s):
    char_set = set()
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Contract window until no duplicates
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        
        # Add current character and update max length
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)
    
    return max_length
```
<!-- tabs:end -->

---

## Max Consecutive Ones III
?> LeetCode: [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/description/) `Medium`

- **Simplified Problem**: Given a binary array nums and an integer k, return the maximum number of consecutive 1's in the array if you can flip at most k 0's.

- **Solution Approach**: Use sliding window to maintain a window with at most k zeros. Expand the window by moving right pointer, contract by moving left pointer when zeros exceed k.

<!-- tabs:start -->
### **Go**
```go
func longestOnes(nums []int, k int) int {
    left := 0
    zeroCount := 0
    maxLength := 0
    
    for right := 0; right < len(nums); right++ {
        // Expand window
        if nums[right] == 0 {
            zeroCount++
        }
        
        // Contract window if too many zeros
        for zeroCount > k {
            if nums[left] == 0 {
                zeroCount--
            }
            left++
        }
        
        // Update max length
        maxLength = max(maxLength, right-left+1)
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
def longestOnes(nums, k):
    left = 0
    zero_count = 0
    max_length = 0
    
    for right in range(len(nums)):
        # Expand window
        if nums[right] == 0:
            zero_count += 1
        
        # Contract window if too many zeros
        while zero_count > k:
            if nums[left] == 0:
                zero_count -= 1
            left += 1
        
        # Update max length
        max_length = max(max_length, right - left + 1)
    
    return max_length
```
<!-- tabs:end -->

---

## Minimum Window Substring
?> LeetCode: [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/) `Hard`

- **Simplified Problem**: Given two strings s and t, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

- **Solution Approach**: Use sliding window with two hash maps to track character frequencies. Expand window until all characters of t are covered, then contract to find minimum window.

<!-- tabs:start -->
### **Go**
```go
func minWindow(s string, t string) string {
    if len(s) < len(t) {
        return ""
    }
    
    // Count characters in t
    tCount := make(map[byte]int)
    for i := 0; i < len(t); i++ {
        tCount[t[i]]++
    }
    
    required := len(tCount)
    formed := 0
    windowCounts := make(map[byte]int)
    
    left, right := 0, 0
    minLen := len(s) + 1
    minLeft := 0
    
    for right < len(s) {
        // Expand window
        char := s[right]
        windowCounts[char]++
        
        if count, exists := tCount[char]; exists && windowCounts[char] == count {
            formed++
        }
        
        // Contract window
        for left <= right && formed == required {
            // Update minimum window
            if right-left+1 < minLen {
                minLen = right - left + 1
                minLeft = left
            }
            
            leftChar := s[left]
            windowCounts[leftChar]--
            if count, exists := tCount[leftChar]; exists && windowCounts[leftChar] < count {
                formed--
            }
            left++
        }
        right++
    }
    
    if minLen == len(s)+1 {
        return ""
    }
    return s[minLeft : minLeft+minLen]
}
```

### **Python**
```python
def minWindow(s, t):
    if len(s) < len(t):
        return ""
    
    from collections import Counter, defaultdict
    
    # Count characters in t
    t_count = Counter(t)
    required = len(t_count)
    
    # Sliding window variables
    left = right = 0
    formed = 0
    window_counts = defaultdict(int)
    
    # Result
    min_len = float('inf')
    min_left = 0
    
    while right < len(s):
        # Expand window
        char = s[right]
        window_counts[char] += 1
        
        if char in t_count and window_counts[char] == t_count[char]:
            formed += 1
        
        # Contract window
        while left <= right and formed == required:
            # Update minimum window
            if right - left + 1 < min_len:
                min_len = right - left + 1
                min_left = left
            
            left_char = s[left]
            window_counts[left_char] -= 1
            if left_char in t_count and window_counts[left_char] < t_count[left_char]:
                formed -= 1
            
            left += 1
        
        right += 1
    
    return "" if min_len == float('inf') else s[min_left:min_left + min_len]
```
<!-- tabs:end -->

---

## Longest Repeating Character Replacement
?> LeetCode: [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/description/) `Medium`

- **Simplified Problem**: Given a string s and an integer k, you can choose any character of the string and change it to any other uppercase English character. Return the length of the longest substring containing the same letter you can get after performing the above operations.

- **Solution Approach**: Use sliding window with character frequency tracking. The key insight is that we need at most k replacements when `window_size - max_frequency <= k`.

<!-- tabs:start -->
### **Go**
```go
func characterReplacement(s string, k int) int {
    charCount := make(map[byte]int)
    left := 0
    maxCount := 0
    maxLength := 0
    
    for right := 0; right < len(s); right++ {
        // Expand window
        charCount[s[right]]++
        maxCount = max(maxCount, charCount[s[right]])
        
        // Contract window if needed
        if right-left+1-maxCount > k {
            charCount[s[left]]--
            left++
        }
        
        // Update max length
        maxLength = max(maxLength, right-left+1)
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
def characterReplacement(s, k):
    from collections import defaultdict
    
    char_count = defaultdict(int)
    left = 0
    max_count = 0
    max_length = 0
    
    for right in range(len(s)):
        # Expand window
        char_count[s[right]] += 1
        max_count = max(max_count, char_count[s[right]])
        
        # Contract window if needed
        if right - left + 1 - max_count > k:
            char_count[s[left]] -= 1
            left += 1
        
        # Update max length
        max_length = max(max_length, right - left + 1)
    
    return max_length
```
<!-- tabs:end -->
# Examples

## Two Sum II - Input Array Is Sorted
?> LeetCode: [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/) `Medium`

- **Simplified Problem**: Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Return their 1-based indices.

- **Solution Approach**: Use two pointers—one starting **from the beginning (left)** and the other **from the end (right)** of the array. Move the pointers towards each other based on the sum of the values at the pointers compared to the target:
```pseudocode
if sum == target {
    return indices
} else if sum < target {
    left++
} else {
    right--
}
```

Here's the complete Solution:

<!-- tabs:start -->
### **Go**
```go
func twoSum(numbers []int, target int) []int {
    left, right := 0, len(numbers)-1
    for left < right {
        sum := numbers[left] + numbers[right]
        if sum == target {
            // as mentioned in the problem, this is a 1-indexed array, so.. :D
            return []int{left+1, right+1}
        } else if sum < target {
            left++
        } else {
            right--
        }
    }
    return []int{}
}
```

### **Python**
```python
def twoSum(numbers, target):
    left, right = 0, len(numbers) - 1
    while left < right:
        sum = numbers[left] + numbers[right]
        if sum == target:
            return [left + 1, right + 1]
        elif sum < target:
            left += 1
        else:
            right -= 1
    return None
```
<!-- tabs:end -->


---

## Remove Duplicates from Sorted Array
?> LeetCode: [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/) `Easy`

- **Simplified Problem**: Given a sorted array nums, remove the duplicates in-place such that each element appears only once and return the new length of the array.

- **Solution Approach**: Use two pointers—one to track the position for the next unique element (slow pointer) and the other to iterate through the array (fast pointer). When a new unique element is found, place it at the slow pointer's position and increment the slow pointer.

<!-- tabs:start -->

#### **Go**
```go
func removeDuplicates(nums []int) int {
    if len(nums) == 0 {
        return 0
    }
    i := 0
    for j := 1; j < len(nums); j++ {
        if nums[j] != nums[i] {
            i++
            nums[i] = nums[j]
        }
    }
    return i + 1
}
```

#### **Python**
```python
def removeDuplicates(nums):
    if not nums:
        return 0
    i = 0
    for j in range(1, len(nums)):
        if nums[j] != nums[i]:
            i += 1
            nums[i] = nums[j]
    return i + 1
```
<!-- tabs:end -->

---

## Valid Palindrome

?> LeetCode: [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/) `Easy`

!> Palindrome /ˈpælɪndrəʊm/

- **Simplified Problem**: Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

- **Solution Approach**: Use two pointers starting from both ends of the string. Skip non-alphanumeric characters and compare the alphanumeric characters (case-insensitive) as the pointers move towards the center. If any pair of characters doesn't match, the string is not a palindrome.

<!-- tabs:start -->
### **Go**
```go
import "strings"

func isPalindrome(s string) bool {
    s = strings.ToLower(s)
    left, right := 0, len(s)-1
    for left < right {
        for left < right && !isAlphanumeric(s[left]) {
            left++
        }
        for left < right && !isAlphanumeric(s[right]) {
            right--
        }
        if left < right && s[left] != s[right] {
            return false
        }
        left++
        right--
    }
    return true
}

func isAlphanumeric(c byte) bool {
    return (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9')
}
```

### **Python**
```python
def isPalindrome(s):
    s = s.lower()
    left, right = 0, len(s) - 1
    while left < right:
        while left < right and not s[left].isalnum():
            left += 1
        while left < right and not s[right].isalnum():
            right -= 1
        if left < right and s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True
```
<!-- tabs:end -->
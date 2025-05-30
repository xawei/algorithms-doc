# Examples

## Binary Search
?> LeetCode: [704. Binary Search](https://leetcode.com/problems/binary-search/description/) `Easy`

- **Simplified Problem**: Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.

- **Solution Approach**: Use the classic binary search template. Compare the middle element with the target and adjust the search boundaries accordingly.

```pseudocode
while left <= right:
    mid = left + (right - left) / 2
    if nums[mid] == target:
        return mid
    else if nums[mid] < target:
        left = mid + 1
    else:
        right = mid - 1
```

<!-- tabs:start -->
### **Go**
```go
func search(nums []int, target int) int {
    left, right := 0, len(nums)-1
    
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            return mid
        } else if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return -1
}
```

### **Python**
```python
def search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```
<!-- tabs:end -->

---

## Search Insert Position
?> LeetCode: [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/description/) `Easy`

- **Simplified Problem**: Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

- **Solution Approach**: Use binary search to find the target or the insertion position. When the loop ends, `left` will be the correct insertion position.

<!-- tabs:start -->
### **Go**
```go
func searchInsert(nums []int, target int) int {
    left, right := 0, len(nums)-1
    
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            return mid
        } else if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return left
}
```

### **Python**
```python
def searchInsert(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return left
```
<!-- tabs:end -->

---

## Find First and Last Position of Element in Sorted Array
?> LeetCode: [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/) `Medium`

- **Simplified Problem**: Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value. If target is not found in the array, return [-1, -1].

- **Solution Approach**: Use two binary searches - one to find the leftmost (first) occurrence and another to find the rightmost (last) occurrence of the target.

<!-- tabs:start -->
### **Go**
```go
func searchRange(nums []int, target int) []int {
    return []int{findFirst(nums, target), findLast(nums, target)}
}

func findFirst(nums []int, target int) int {
    left, right := 0, len(nums)-1
    result := -1
    
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            result = mid
            right = mid - 1  // Continue searching left
        } else if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return result
}

func findLast(nums []int, target int) int {
    left, right := 0, len(nums)-1
    result := -1
    
    for left <= right {
        mid := left + (right-left)/2
        if nums[mid] == target {
            result = mid
            left = mid + 1  // Continue searching right
        } else if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }
    return result
}
```

### **Python**
```python
def searchRange(nums, target):
    def findFirst(nums, target):
        left, right = 0, len(nums) - 1
        result = -1
        
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                result = mid
                right = mid - 1  # Continue searching left
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        
        return result
    
    def findLast(nums, target):
        left, right = 0, len(nums) - 1
        result = -1
        
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                result = mid
                left = mid + 1  # Continue searching right
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        
        return result
    
    return [findFirst(nums, target), findLast(nums, target)]
```
<!-- tabs:end -->

---

## Search in Rotated Sorted Array
?> LeetCode: [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/) `Medium`

- **Simplified Problem**: Given a rotated sorted array and a target value, search for the target. If found, return its index, otherwise return -1.

- **Solution Approach**: Use modified binary search. At each step, determine which half is properly sorted, then decide which half to search based on the target's relationship with the sorted half.

<!-- tabs:start -->
### **Go**
```go
func search(nums []int, target int) int {
    left, right := 0, len(nums)-1
    
    for left <= right {
        mid := left + (right-left)/2
        
        if nums[mid] == target {
            return mid
        }
        
        // Check if left half is sorted
        if nums[left] <= nums[mid] {
            if nums[left] <= target && target < nums[mid] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else { // Right half is sorted
            if nums[mid] < target && target <= nums[right] {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }
    return -1
}
```

### **Python**
```python
def search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        
        # Check if left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # Right half is sorted
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    
    return -1
```
<!-- tabs:end --> 
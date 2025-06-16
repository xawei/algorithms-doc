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
// https://www.youtube.com/watch?v=4sQL7R5ySUU&ab_channel=NeetCode

func searchRange(nums []int, target int) []int {
    leftMostIndex := binarySearch(nums, target, true)
    rightMostIndex := binarySearch(nums, target, false)
    return []int{leftMostIndex, rightMostIndex}
}

func binarySearch(nums []int, target int, leftMost bool) int {
    l, r := 0, len(nums)-1
    ans := -1 // this is the key point
    for l <= r {
        mid := (l+r) / 2
        if nums[mid] < target {
            l = mid + 1
        } else if nums[mid] > target {
            r = mid - 1
        } else {
            // normal binary search end here. But as we need to find the left most or right most index, we need to keep moving l or r until they exceed each other.
            ans = mid
            if leftMost {
                r = mid - 1
            } else {
                l = mid + 1
            }
        }
    }
    return ans
}
```

### **Python**
```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        leftMost = self.binarySearch(nums, target, True)
        rightMost = self.binarySearch(nums, target, False)
        return [leftMost, rightMost]

    def binarySearch(self, nums: List[int], target: int, leftMost: bool) -> int:
        l, r = 0, len(nums)-1
        ans = -1
        while l <= r:
            mid = (l + r) // 2
            if target < nums[mid]:
                r = mid - 1
            elif target > nums[mid]:
                l = mid + 1
            else:
                ans = mid
                if leftMost:
                    r = mid - 1
                else:
                    l = mid + 1
        return ans
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
        if nums[left] <= nums[mid] { // ⚠️ can't use nums[left] < nums[mid] here, we have to make sure left half is sorted (even if it has 1 item)
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
# Examples of Fast and Slow Pointers in Action

## Linked List Cycle
?> LeetCode: [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

### *Floyd's Cycle Detection*

![Floyd's Cycle Detection](https://blog202411-1252613377.cos.ap-guangzhou.myqcloud.com/floyd's%20cycle%20detection%20algorithm.png ':size=100%')

- **Simplified Problem**: Given the head of a linked list, determine if the list contains a cycle.

- **Solution Approach**: `Floyd's Cycle Detection`. Use two pointers—`slow` moves one step at a time, and `fast` moves two steps. If there's a cycle, the fast pointer will eventually meet the slow pointer. If not, the fast pointer will reach the end.

<!-- tabs:start -->
### **Go**
```go
func hasCycle(head *ListNode) bool {
    if head == nil {
        return false
    }
    s, f := head, head.Next
    for f!= nil && f.Next!=nil && s != f {
        s = s.Next
        f = f.Next.Next
    }
    if f == nil || f.Next == nil {
        return false
    } else {
        return true
    }
}
```

### **Python**
```python
def hasCycle(head):
    if not head or not head.next:
        return False
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```
<!-- tabs:end -->

## Middle of the Linked List
?> LeetCode: [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/description/) `Easy`
- **Simplified Problem**: Find the middle node of a singly linked list. If there are two middle nodes, return the second one.

- **Solution Approach**: Use slow (one step) and fast (two steps). When fast reaches the end, slow is at the middle.

<!-- tabs:start -->

### **Go**
```go
func middleNode(head *ListNode) *ListNode {
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    return slow
}
```

### **Python**
```python
func middleNode(head *ListNode) *ListNode {
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    return slow
}
```
<!-- tabs:end -->

## Find the Duplicate Number
?> LeetCode: [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/description/) `Medium`

!> This one is a bit tricky 🤔, but can use it as a good example to think of the relationship between array and linked list  
[NeetCode explanation](https://www.youtube.com/watch?app=desktop&v=wjYnzkAhcNk&ab_channel=NeetCode)  
The NeetCode explanation video is a bit tedious, pls watch it only if you really have no Idea. Anyway, long story short: Firstly, **recognize the problem as a Linked List problem**. Secondary, **use Floyd's Cycle detection algorithm**.



An interesting Video from *Joma Tech* 😄

[youtube video](https://www.youtube.com/embed/pKO9UjSeLew?si=2BiYnN6_liq5-SjF ':include :type=iframe width=100% height=400px allowfullscreen')

- **Simplified Problem**: Find the duplicate in an array of n + 1 integers between 1 and n, using constant space.

- **Solution Approach**: Treat the array as a linked list with a cycle. Use fast and slow pointers to find the cycle's start (duplicate).

<!-- tabs:start -->
### **Go**
```go
func findDuplicate(nums []int) int {
    s, f := 0, 0
    for s == 0 || s != f { // the integer is in the range [1,n], won't be 0
        s = nums[s]
        f = nums[nums[f]]
    }

    s = 0
    for s != f {
        s = nums[s]
        f = nums[f]
    }
    return s
}
```

### **Python**
```python
def findDuplicate(nums):
    slow, fast = nums[0], nums[0]
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
    return slow
```
<!-- tabs:end -->
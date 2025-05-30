# Examples

## Kth Largest Element in an Array
?> LeetCode: [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/) `Medium`

- **Simplified Problem**: Find the kth largest element in an unsorted array. Note that it is the kth largest element in sorted order, not the kth distinct element.

- **Solution Approach**: Use a min-heap of size K. The root of this heap will always be the Kth largest element seen so far.

```pseudocode
kthLargest(nums, k):
    heap = min_heap()
    for num in nums:
        heap.push(num)
        if heap.size() > k:
            heap.pop()  // Remove smallest
    return heap.top()   // Kth largest
```

<!-- tabs:start -->
### **Go**
```go
import "container/heap"

type IntHeap []int

func (h IntHeap) Len() int           { return len(h) }
func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] } // Min heap
func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *IntHeap) Push(x interface{}) {
    *h = append(*h, x.(int))
}

func (h *IntHeap) Pop() interface{} {
    old := *h
    n := len(old)
    x := old[n-1]
    *h = old[0 : n-1]
    return x
}

func findKthLargest(nums []int, k int) int {
    h := &IntHeap{}
    heap.Init(h)
    
    for _, num := range nums {
        heap.Push(h, num)
        if h.Len() > k {
            heap.Pop(h)
        }
    }
    
    return (*h)[0] // Root of min heap is Kth largest
}
```

### **Python**
```python
import heapq

def findKthLargest(nums, k):
    heap = []
    
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)
    
    return heap[0]  # Root of min heap is Kth largest
```
<!-- tabs:end -->

---

## Top K Frequent Elements
?> LeetCode: [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/) `Medium`

- **Simplified Problem**: Given an integer array nums and an integer k, return the k most frequent elements.

- **Solution Approach**: First count frequencies, then use a min-heap to keep track of the K most frequent elements.

<!-- tabs:start -->
### **Go**
```go
import (
    "container/heap"
)

type FreqHeap [][2]int // [frequency, element]

func (h FreqHeap) Len() int           { return len(h) }
func (h FreqHeap) Less(i, j int) bool { return h[i][0] < h[j][0] } // Min heap by frequency
func (h FreqHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *FreqHeap) Push(x interface{}) {
    *h = append(*h, x.([2]int))
}

func (h *FreqHeap) Pop() interface{} {
    old := *h
    n := len(old)
    x := old[n-1]
    *h = old[0 : n-1]
    return x
}

func topKFrequent(nums []int, k int) []int {
    // Count frequencies
    freqMap := make(map[int]int)
    for _, num := range nums {
        freqMap[num]++
    }
    
    h := &FreqHeap{}
    heap.Init(h)
    
    // Use min heap to keep K most frequent
    for num, freq := range freqMap {
        heap.Push(h, [2]int{freq, num})
        if h.Len() > k {
            heap.Pop(h)
        }
    }
    
    // Extract elements from heap
    result := make([]int, k)
    for i := 0; i < k; i++ {
        result[i] = (*h)[i][1]
    }
    
    return result
}
```

### **Python**
```python
import heapq
from collections import Counter

def topKFrequent(nums, k):
    # Count frequencies
    freq_map = Counter(nums)
    
    heap = []
    
    # Use min heap to keep K most frequent
    for num, freq in freq_map.items():
        heapq.heappush(heap, (freq, num))
        if len(heap) > k:
            heapq.heappop(heap)
    
    # Extract elements from heap
    return [item[1] for item in heap]
```
<!-- tabs:end -->

---

## K Closest Points to Origin
?> LeetCode: [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/) `Medium`

- **Simplified Problem**: Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

- **Solution Approach**: Use a max-heap to keep track of the K closest points. The heap stores distances with their corresponding points.

<!-- tabs:start -->
### **Go**
```go
import (
    "container/heap"
)

type PointHeap [][3]int // [distance_squared, x, y]

func (h PointHeap) Len() int           { return len(h) }
func (h PointHeap) Less(i, j int) bool { return h[i][0] > h[j][0] } // Max heap by distance
func (h PointHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *PointHeap) Push(x interface{}) {
    *h = append(*h, x.([3]int))
}

func (h *PointHeap) Pop() interface{} {
    old := *h
    n := len(old)
    x := old[n-1]
    *h = old[0 : n-1]
    return x
}

func kClosest(points [][]int, k int) [][]int {
    h := &PointHeap{}
    heap.Init(h)
    
    for _, point := range points {
        x, y := point[0], point[1]
        dist := x*x + y*y // Distance squared
        
        heap.Push(h, [3]int{dist, x, y})
        if h.Len() > k {
            heap.Pop(h)
        }
    }
    
    result := make([][]int, k)
    for i := 0; i < k; i++ {
        point := (*h)[i]
        result[i] = []int{point[1], point[2]}
    }
    
    return result
}
```

### **Python**
```python
import heapq

def kClosest(points, k):
    heap = []
    
    for x, y in points:
        dist = x * x + y * y  # Distance squared
        
        heapq.heappush(heap, (-dist, x, y))  # Negative for max heap
        if len(heap) > k:
            heapq.heappop(heap)
    
    return [[x, y] for _, x, y in heap]
```
<!-- tabs:end -->

---

## Merge k Sorted Lists
?> LeetCode: [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/) `Hard`

- **Simplified Problem**: You are given an array of k linked-lists lists, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list and return it.

- **Solution Approach**: Use a min-heap to always get the smallest current value among all lists. Add the next node from the same list back to the heap.

<!-- tabs:start -->
### **Go**
```go
import "container/heap"

type ListNode struct {
    Val  int
    Next *ListNode
}

type NodeHeap []*ListNode

func (h NodeHeap) Len() int           { return len(h) }
func (h NodeHeap) Less(i, j int) bool { return h[i].Val < h[j].Val }
func (h NodeHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *NodeHeap) Push(x interface{}) {
    *h = append(*h, x.(*ListNode))
}

func (h *NodeHeap) Pop() interface{} {
    old := *h
    n := len(old)
    x := old[n-1]
    *h = old[0 : n-1]
    return x
}

func mergeKLists(lists []*ListNode) *ListNode {
    h := &NodeHeap{}
    heap.Init(h)
    
    // Add first node from each list to heap
    for _, list := range lists {
        if list != nil {
            heap.Push(h, list)
        }
    }
    
    dummy := &ListNode{}
    current := dummy
    
    for h.Len() > 0 {
        // Get smallest node
        node := heap.Pop(h).(*ListNode)
        current.Next = node
        current = current.Next
        
        // Add next node from same list
        if node.Next != nil {
            heap.Push(h, node.Next)
        }
    }
    
    return dummy.Next
}
```

### **Python**
```python
import heapq

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
    
    def __lt__(self, other):
        return self.val < other.val

def mergeKLists(lists):
    heap = []
    
    # Add first node from each list to heap
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst.val, i, lst))
    
    dummy = ListNode()
    current = dummy
    
    while heap:
        # Get smallest node
        val, i, node = heapq.heappop(heap)
        current.next = node
        current = current.next
        
        # Add next node from same list
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    
    return dummy.next
```
<!-- tabs:end --> 
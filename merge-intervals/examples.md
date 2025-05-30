# Examples

## Merge Intervals
?> LeetCode: [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/description/) `Medium`

- **Simplified Problem**: Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

- **Solution Approach**: Sort intervals by start time, then iterate through them. If the current interval overlaps with the previous one (current start ≤ previous end), merge them by updating the end time.

```pseudocode
sort intervals by start time
result = [first interval]
for each remaining interval:
    if interval overlaps with last in result:
        merge them by updating the end time
    else:
        add interval to result
```

<!-- tabs:start -->
### **Go**
```go
import "sort"

func merge(intervals [][]int) [][]int {
    if len(intervals) <= 1 {
        return intervals
    }
    
    // Sort by start time
    sort.Slice(intervals, func(i, j int) bool {
        return intervals[i][0] < intervals[j][0]
    })
    
    result := [][]int{intervals[0]}
    
    for i := 1; i < len(intervals); i++ {
        current := intervals[i]
        last := result[len(result)-1]
        
        // Check if current interval overlaps with last merged interval
        if current[0] <= last[1] {
            // Merge intervals by updating end time
            last[1] = max(last[1], current[1])
        } else {
            // No overlap, add current interval
            result = append(result, current)
        }
    }
    
    return result
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
def merge(intervals):
    if len(intervals) <= 1:
        return intervals
    
    # Sort by start time
    intervals.sort(key=lambda x: x[0])
    
    result = [intervals[0]]
    
    for i in range(1, len(intervals)):
        current = intervals[i]
        last = result[-1]
        
        # Check if current interval overlaps with last merged interval
        if current[0] <= last[1]:
            # Merge intervals by updating end time
            last[1] = max(last[1], current[1])
        else:
            # No overlap, add current interval
            result.append(current)
    
    return result
```
<!-- tabs:end -->

---

## Insert Interval
?> LeetCode: [57. Insert Interval](https://leetcode.com/problems/insert-interval/description/) `Medium`

- **Simplified Problem**: Given a set of non-overlapping intervals sorted by their start time, insert a new interval and merge if necessary.

- **Solution Approach**: Add all intervals that end before the new interval starts, then merge all overlapping intervals with the new interval, and finally add all intervals that start after the new interval ends.

<!-- tabs:start -->
### **Go**
```go
func insert(intervals [][]int, newInterval []int) [][]int {
    result := [][]int{}
    i := 0
    n := len(intervals)
    
    // Add all intervals that end before newInterval starts
    for i < n && intervals[i][1] < newInterval[0] {
        result = append(result, intervals[i])
        i++
    }
    
    // Merge all overlapping intervals with newInterval
    for i < n && intervals[i][0] <= newInterval[1] {
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i++
    }
    result = append(result, newInterval)
    
    // Add all intervals that start after newInterval ends
    for i < n {
        result = append(result, intervals[i])
        i++
    }
    
    return result
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
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
def insert(intervals, newInterval):
    result = []
    i = 0
    n = len(intervals)
    
    # Add all intervals that end before newInterval starts
    while i < n and intervals[i][1] < newInterval[0]:
        result.append(intervals[i])
        i += 1
    
    # Merge all overlapping intervals with newInterval
    while i < n and intervals[i][0] <= newInterval[1]:
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i += 1
    result.append(newInterval)
    
    # Add all intervals that start after newInterval ends
    while i < n:
        result.append(intervals[i])
        i += 1
    
    return result
```
<!-- tabs:end -->

---

## Meeting Rooms
?> LeetCode: [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms/description/) `Easy`

- **Simplified Problem**: Given an array of meeting time intervals consisting of start and end times, determine if a person could attend all meetings (i.e., no two meetings overlap).

- **Solution Approach**: Sort meetings by start time, then check if any meeting starts before the previous one ends.

<!-- tabs:start -->
### **Go**
```go
import "sort"

func canAttendMeetings(intervals [][]int) bool {
    if len(intervals) <= 1 {
        return true
    }
    
    // Sort by start time
    sort.Slice(intervals, func(i, j int) bool {
        return intervals[i][0] < intervals[j][0]
    })
    
    // Check for overlaps
    for i := 1; i < len(intervals); i++ {
        if intervals[i][0] < intervals[i-1][1] {
            return false // Overlap found
        }
    }
    
    return true
}
```

### **Python**
```python
def canAttendMeetings(intervals):
    if len(intervals) <= 1:
        return True
    
    # Sort by start time
    intervals.sort(key=lambda x: x[0])
    
    # Check for overlaps
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i-1][1]:
            return False  # Overlap found
    
    return True
```
<!-- tabs:end -->

---

## Meeting Rooms II
?> LeetCode: [253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/description/) `Medium`

- **Simplified Problem**: Given an array of meeting time intervals, find the minimum number of conference rooms required.

- **Solution Approach**: Use two pointers technique with sorted start and end times. Count how many meetings are happening simultaneously by tracking when meetings start and end.

<!-- tabs:start -->
### **Go**
```go
import "sort"

func minMeetingRooms(intervals [][]int) int {
    if len(intervals) == 0 {
        return 0
    }
    
    n := len(intervals)
    starts := make([]int, n)
    ends := make([]int, n)
    
    // Extract start and end times
    for i, interval := range intervals {
        starts[i] = interval[0]
        ends[i] = interval[1]
    }
    
    // Sort both arrays
    sort.Ints(starts)
    sort.Ints(ends)
    
    rooms := 0
    maxRooms := 0
    startPtr := 0
    endPtr := 0
    
    // Use two pointers to count concurrent meetings
    for startPtr < n {
        if starts[startPtr] < ends[endPtr] {
            rooms++
            maxRooms = max(maxRooms, rooms)
            startPtr++
        } else {
            rooms--
            endPtr++
        }
    }
    
    return maxRooms
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
def minMeetingRooms(intervals):
    if not intervals:
        return 0
    
    n = len(intervals)
    starts = sorted([interval[0] for interval in intervals])
    ends = sorted([interval[1] for interval in intervals])
    
    rooms = 0
    max_rooms = 0
    start_ptr = 0
    end_ptr = 0
    
    # Use two pointers to count concurrent meetings
    while start_ptr < n:
        if starts[start_ptr] < ends[end_ptr]:
            rooms += 1
            max_rooms = max(max_rooms, rooms)
            start_ptr += 1
        else:
            rooms -= 1
            end_ptr += 1
    
    return max_rooms
```
<!-- tabs:end --> 
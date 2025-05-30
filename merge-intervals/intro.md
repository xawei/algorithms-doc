# Merge Intervals

The Merge Intervals pattern is used to deal with **overlapping intervals** and is particularly useful for problems involving scheduling, time management, or any scenario where you need to **consolidate overlapping ranges**. The key insight is to first sort intervals by their start time, then iterate through them to merge overlapping ones.

## When to Use Merge Intervals

This pattern is ideal for problems where you need to:

- **Merge overlapping intervals**: Combining time slots, meeting rooms, or any overlapping ranges.
- **Find gaps between intervals**: Identifying free time slots or missing ranges.
- **Insert new intervals**: Adding new intervals while maintaining a merged list.
- **Count overlapping intervals**: Determining maximum number of concurrent events.

## Why Use Merge Intervals?

- **Simplifies complex scheduling**: Reduces overlapping intervals to a simpler, non-overlapping set.
- **Efficient time complexity**: Usually O(n log n) due to sorting, with O(n) for the merging process.
- **Clear algorithm pattern**: Sort by start time, then merge overlapping intervals.
- **Space efficient**: Often can be done in-place or with minimal extra space.

## Common Use Cases

1. **Meeting Rooms**: Determining if meeting times conflict or merging overlapping meetings.
2. **Calendar Integration**: Merging calendars from different sources.
3. **Resource Allocation**: Optimizing time slot usage for shared resources.
4. **Range Merging**: Combining overlapping number ranges or date ranges.
5. **Scheduling**: Finding available time slots or optimizing schedules. 
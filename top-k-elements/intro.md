# Top K Elements (Heap/Priority Queue)

The **Top K Elements** pattern is a powerful technique that uses **heaps** (priority queues) to efficiently find, maintain, or process the **K largest**, **K smallest**, or **K most frequent** elements in a dataset. This pattern is particularly valuable when you need to track extremes in a stream of data or when sorting the entire dataset would be overkill.

## When to Use Top K Elements

This pattern is ideal for problems where you need to:

- **Find K largest/smallest elements**: Without sorting the entire array.
- **Track top K in a stream**: Maintaining K best elements as data arrives.
- **K most/least frequent**: Finding elements that appear most or least often.
- **K closest points**: Finding nearest neighbors or closest distances.
- **Merge K sorted lists**: Efficiently combining multiple sorted sequences.

## Why Use Heaps?

- **Time efficiency**: O(N log K) vs O(N log N) for full sorting.
- **Space efficiency**: Only need to store K elements, not the entire dataset.
- **Real-time processing**: Can handle streaming data efficiently.
- **Flexible retrieval**: Easy to get min/max without recomputing.

## Key Concepts

### Min Heap vs Max Heap
- **Min Heap**: Root is the smallest element (use for K largest problems)
- **Max Heap**: Root is the largest element (use for K smallest problems)
- **Counter-intuitive but correct**: Use min heap to find K largest by keeping only the K largest seen so far

### Common Heap Operations
- **Insert**: Add element (O(log K))
- **Extract**: Remove root element (O(log K))
- **Peek**: View root without removing (O(1))
- **Size Management**: Keep heap size ≤ K

## Common Use Cases

1. **Top K Frequent**: Find most frequent elements in an array.
2. **Kth Largest**: Find the Kth largest element in an array.
3. **K Closest Points**: Find K nearest points to origin.
4. **Merge K Lists**: Combine K sorted linked lists.
5. **Running Median**: Maintain median in a data stream. 
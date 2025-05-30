# Binary Search

Binary Search is an efficient algorithm for finding a target value in a **sorted array** by repeatedly dividing the search interval in half. If the target value is less than the middle element, the search continues in the lower half; otherwise, it continues in the upper half. This process eliminates half of the remaining elements with each comparison.

## When to Use Binary Search

Binary Search is perfect for problems where you need to:

- **Search in sorted arrays**: Finding a specific element in a sorted collection.
- **Find boundaries**: Such as the first or last occurrence of a target value.
- **Search in solution space**: Problems where you can determine if a solution exists within a range.
- **Optimize decision problems**: Where you need to find the minimum or maximum value that satisfies certain conditions.

## Why Use Binary Search?

- **Time efficiency**: Reduces time complexity from O(n) to O(log n) for search operations.
- **Space efficient**: Uses constant extra space O(1) in iterative implementation.
- **Predictable performance**: Consistent logarithmic time complexity regardless of data distribution.
- **Versatile**: Can be adapted for various search and optimization problems.

## Common Use Cases

1. **Classic Search**: Finding an element in a sorted array.
2. **Find First/Last**: Locating the first or last occurrence of a duplicate element.
3. **Search Insert Position**: Finding where to insert an element to maintain sorted order.
4. **Peak Finding**: Finding local maximums in arrays or matrices.
5. **Search in Rotated Arrays**: Modified binary search for rotated sorted arrays. 
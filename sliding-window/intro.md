# Sliding Window

The Sliding Window technique is a widely used algorithmic pattern for **solving problems involving sequences like arrays or strings**. It works by maintaining a "window" of elements that slides across the data, expanding or contracting as needed to meet specific conditions. This approach is prized for its ability to transform inefficient brute-force solutions into optimized ones, often reducing time complexity from O(n²) to O(n).

In programming, the sliding window uses two pointers (typically "left" and "right") to define the boundaries of this subset, adjusting them dynamically based on the problem's requirements.

## When to Use It

The sliding window pattern shines in scenarios like:

- Finding the longest substring with unique characters.
- Identifying the smallest window containing a set of target elements.
- Computing maximum or minimum values over a fixed-size subarray.
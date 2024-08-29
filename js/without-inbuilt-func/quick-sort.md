# Quick Sort Implementation in JavaScript

Quick Sort is an efficient, in-place sorting algorithm that, on average, makes O(n log n) comparisons to sort an array of n elements. It is a divide-and-conquer algorithm and is widely used due to its efficiency in practice.

## Quick Sort Algorithm

1. **Choose a Pivot**: Select an element from the array as the pivot. There are various strategies for choosing the pivot, such as picking the first element, the last element, the middle element, or a random element.
  
2. **Partitioning**: Reorder the array so that all elements with values less than the pivot come before the pivot, and all elements with values greater than the pivot come after it. After this partitioning, the pivot is in its final position. This step is called the partition operation.
  
3. **Recursively Apply**: Recursively apply the above steps to the subarray of elements with smaller values and the subarray of elements with greater values.

## Implementation

Below is a JavaScript implementation of the Quick Sort algorithm:

```javascript
function quickSort(arr) {
  // Base case: If the array has 1 or 0 elements, it is already sorted
  if (arr.length <= 1) {
    return arr;
  }

  // Choose the pivot (using the last element for simplicity)
  let pivot = arr[arr.length - 1];
  let left = [];
  let right = [];

  // Partition the array into left and right arrays
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  // Recursively apply quick sort to left and right arrays, then concatenate
  return [...quickSort(left), pivot, ...quickSort(right)];
}

// Test the function
let nums1 = [5, 2, 3, 1];
console.log(quickSort(nums1)); // Output: [1, 2, 3, 5]

let nums2 = [5, 1, 1, 2, 0, 0];
console.log(quickSort(nums2)); // Output: [0, 0, 1, 1, 2, 5]

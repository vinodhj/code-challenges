## Problem: `inorderTraversal` Generator Function

Create a generator function called `inorderTraversal` that yields integers from a multi-dimensional array in the order of an inorder traversal.

### Example

```javascript
const multiDimArray = [
  [1, [2, 3]],
  [4, [5, [6, 7]]],
];

function* inorderTraversal(arr) {
  // Implement the generator function here
   for (let item of arr) {
        if (Array.isArray(item)) {
            yield* inorderTraversal(item);
        }else{
            yield item;
        }
    }
}

// Usage
const iterator = inorderTraversal(multiDimArray);
console.log([...iterator]); // Output: [1, 2, 3, 4, 5, 6, 7]

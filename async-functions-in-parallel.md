# `promiseAll` Function

## Problem Statement

Given an array of asynchronous functions `functions`, return a new promise `promise`. Each function in the array accepts no arguments and returns a promise. All the promises should be executed in parallel.

### The `promise` resolves:
- When all the promises returned from `functions` were resolved successfully in parallel.
- The resolved value of `promise` should be an array of all the resolved values of promises in the same order as they were in the `functions`.
- The `promise` should resolve when all the asynchronous functions in the array have completed execution in parallel.

### The `promise` rejects:
- When any of the promises returned from `functions` were rejected.
- `promise` should also reject with the reason for the first rejection.

### Constraints:
- You must solve it without using the built-in `Promise.all` function.
- `functions` is an array of functions that return promises.
- `1 <= functions.length <= 10`.

## Solution

```javascript
function promiseAll(functions) {
    return new Promise((resolve, reject) => {
        const results = [];
        let completedPromises = 0;
        let hasRejected = false;

        functions.forEach((fn, index) => {
            fn().then((result) => {
                if (hasRejected) return;
                results[index] = result;
                completedPromises += 1;

                if (completedPromises === functions.length) {
                    resolve(results);
                }
            }).catch((err) => {
                if (!hasRejected) {
                    hasRejected = true;
                    reject(err);
                }
            });
        });
    });
}


// Example 1
const functions = [
  () => new Promise(resolve => setTimeout(() => resolve(5), 200))
];

promiseAll(functions).then(console.log); // Output: [5]

// Example 2
const functions = [
  () => new Promise(resolve => setTimeout(() => resolve(1), 200)), 
  () => new Promise((resolve, reject) => setTimeout(() => reject("Error"), 100))
];

promiseAll(functions)
  .then(console.log)
  .catch(console.error); // Output: "Error"

// Example 3
const functions = [
  () => new Promise(resolve => setTimeout(() => resolve(4), 50)), 
  () => new Promise(resolve => setTimeout(() => resolve(10), 150)), 
  () => new Promise(resolve => setTimeout(() => resolve(16), 100))
];

promiseAll(functions).then(console.log); // Output: [4, 10, 16]


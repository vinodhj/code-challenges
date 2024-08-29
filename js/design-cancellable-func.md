
# Cancellable Generator Function

## Overview

This markdown file details an implementation of a cancellable generator function that handles long-running tasks. The function `cancellable` accepts a generator object and returns an array of two values: a cancel function and a promise. The generator function yields promises, and the `cancellable` function manages the resolution of these promises, including handling cancellations and errors.

## Implementation

```javascript
var cancellable = function (generator) {
    let cancel;
    let cancelPromise = new Promise((_, reject) => {
        cancel = () => reject("Cancelled");
    });
    
    cancelPromise.catch(() => { /* Silence unhandled rejection */ });

    const generatorPromise = (async () => {
        let next;
        
        try {
            // Start the generator
            next = generator.next();
            while (!next.done) {
                // Wait for the next promise to resolve or for cancellation
                next = generator.next(await Promise.race([next.value, cancelPromise]));
            }
        } catch (e) {
            // If an error occurs, throw it back into the generator
            try {
                next = generator.throw(e);
                while (!next.done) {
                    // Continue processing until generator is done
                    next = generator.next(await Promise.race([next.value, cancelPromise]));
                }
            } catch (finalError) {
                // If generator throws again, reject with that error
                return Promise.reject(finalError);
            }
        }
        
        // If generator completes successfully, return its final value
        return next.value;
    })();

    return [cancel, generatorPromise];
};
```

## Explanation

### 1. **Promise Race for Cancellation**
   - The `Promise.race([next.value, cancelPromise])` is crucial for handling cancellation. It ensures that either the promise yielded by the generator resolves, or the `cancelPromise` rejects (indicating cancellation). This allows for immediate interruption of the generator's execution when the `cancel()` function is invoked.

### 2. **Error Handling**
   - The implementation wraps the generator's execution in a `try...catch` block. If an error is thrown, it's passed back to the generator using `generator.throw(e)`. This allows the generator to handle the error as it sees fit (e.g., through internal `try...catch` blocks). If the generator throws again, the error is caught and the promise returned by the `cancellable` function is rejected with that error.

### 3. **Handling Completion**
   - The generator continues to execute until it's done (`next.done` is `true`). The final value returned by the generator is then resolved by the promise returned by the `cancellable` function.

### 4. **Silencing Unhandled Rejection**
   - The `cancelPromise.catch(() => { /* Silence unhandled rejection */ });` line is used to avoid unhandled promise rejection warnings, which could occur if `cancel()` is called after the generator has completed.

## Use Cases and Examples

The following use cases demonstrate how the `cancellable` function can be used in practice:

### Use Case 4: Passing the Case
**Input:**
```javascript
function*() { 
    let result = 0; 
    try { 
        yield new Promise(res => setTimeout(res, 100)); 
        result += yield new Promise(res => res(1)); 
        yield new Promise(res => setTimeout(res, 100)); 
        result += yield new Promise(res => res(1)); 
    } catch(e) { 
        return result; 
    } 
    return result; 
}
cancelledAt = 150;
```
**Expected Output:**
```json
{"resolved":1}
```

**Explanation:**
The generator successfully catches the cancellation error and returns the result up to that point.

### Use Case 5: Failing Case
**Input:**
```javascript
function*() { 
    try { 
        yield new Promise((resolve, reject) => reject("Promise Rejected")); 
    } catch(e) { 
        let a = yield new Promise(resolve => resolve(2)); 
        let b = yield new Promise(resolve => resolve(2)); 
        return a + b; 
    } 
}
cancelledAt = null;
```
**Expected Output:**
```json
{"resolved":4}
```

**Explanation:**
The generator catches the initial rejection, continues processing, and eventually resolves with a value of 4.

## Summary

This implementation of `cancellable` properly handles long-running tasks that can be interrupted or cancelled. It ensures that the generator's flow continues correctly even after errors or cancellations, making it robust and suitable for various asynchronous tasks that require fine-grained control over their execution.

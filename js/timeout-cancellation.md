# Cancellable Function Implementation

## Problem Statement

Given a function `fn`, an array of arguments `args`, and a timeout `t` in milliseconds, return a cancel function `cancelFn`.

The execution of `fn` should be delayed by `t` milliseconds. If `cancelFn` is invoked before `t` milliseconds, it should cancel the delayed execution of `fn`. Otherwise, `fn` should be executed with the provided `args` as arguments.

## Implementation

```javascript
function cancellable(fn, args, t) {
    // Create a timeout for the function execution
    const timeoutId = setTimeout(() => {
        fn(...args);  // Execute the function with the provided arguments
    }, t);

    // Return a function that can cancel the above timeout
    return function cancelFn() {
        clearTimeout(timeoutId);  // Cancel the timeout
    };
}

// Example usage:
const fn1 = (x) => x * 5;
const args1 = [2];
const t1 = 20;
const cancelFn1 = cancellable(fn1, args1, t1);
setTimeout(cancelFn1, 50);  // This will cancel the execution of fn1 before 20ms

const fn2 = (x) => x**2;
const args2 = [2];
const t2 = 100;
const cancelFn2 = cancellable(fn2, args2, t2);
setTimeout(cancelFn2, 50);  // This will cancel the execution of fn2 before 100ms

const fn3 = (x1, x2) => x1 * x2;
const args3 = [2, 4];
const t3 = 30;
const cancelFn3 = cancellable(fn3, args3, t3);
setTimeout(cancelFn3, 100);  // This will NOT cancel fn3 since it's after 30ms


/**
 *  const result = [];
 *
 *  const fn = (x) => x * 5;
 *  const args = [2], t = 20, cancelTimeMs = 50;
 *
 *  const start = performance.now();
 *
 *  const log = (...argsArr) => {
 *      const diff = Math.floor(performance.now() - start);
 *      result.push({"time": diff, "returned": fn(...argsArr)});
 *  }
 *       
 *  const cancel = cancellable(log, args, t);
 *
 *  const maxT = Math.max(t, cancelTimeMs);
 *           
 *  setTimeout(cancel, cancelTimeMs);
 *
 *  setTimeout(() => {
 *      console.log(result); // [{"time":20,"returned":10}]
 *  }, maxT + 15)
 */
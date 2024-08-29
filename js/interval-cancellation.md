## Cancellable Function

### Description

The `cancellable` function schedules a function `fn` to be called with arguments `args` immediately and then repeatedly every `t` milliseconds. It returns a `cancelFn` function that stops further calls after being invoked.

### Code

```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function(fn, args, t) {
    const result = [];
    const startTime = Date.now(); // Capture start time

    // Initial call immediately
    result.push({"time": 0, "returned": fn(...args)});

    const intervalId = setInterval(() => {
        const currentTime = Date.now();
        const elapsed = currentTime - startTime;
        const returned = fn(...args);
        result.push({"time": elapsed, "returned": returned});
    }, t);

    const cancelFn = () => {
        clearInterval(intervalId);
    };

    return cancelFn;
};

// Example Usage
const result = [];

const fn = (x) => x * 2;
const args = [4], t = 35, cancelTimeMs = 190;

const cancel = cancellable(fn, args, t);

setTimeout(cancel, cancelTimeMs);

setTimeout(() => {
    console.log(result); // Expected Output:
                         // [
                         //     {"time":0,"returned":8},
                         //     {"time":36,"returned":8},
                         //     {"time":71,"returned":8},
                         //     {"time":106,"returned":8},
                         //     {"time":142,"returned":8},
                         //     {"time":177,"returned":8}
                         // ]
}, cancelTimeMs + t + 15);
```

## Explanation

- **Initial Call:** 
    The function fn is called immediately when cancellable is invoked. The time is recorded as 0.
- **Subsequent Calls:** 
    fn is called every t milliseconds using setInterval.
- **Cancellation:** 
    The cancelFn function stops further calls when invoked, using clearInterval.
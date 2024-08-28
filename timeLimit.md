# `timeLimit` Function

## Problem Statement

Given an asynchronous function `fn` and a time `t` in milliseconds, return a new time-limited version of the input function. The time-limited function should adhere to the following rules:

1. If `fn` completes within the time limit of `t` milliseconds, the time-limited function should resolve with the result.
2. If the execution of `fn` exceeds the time limit, the time-limited function should reject with the string `"Time Limit Exceeded"`.


## Solution

```javascript
function timeLimit(fn, t) {
    return async function(...args) {
        return new Promise((resolve, reject) => {
            const timer = setTimeout(() => {
                reject("Time Limit Exceeded");
            }, t);

            fn(...args)
                .then((result) => {
                    clearTimeout(timer);
                    resolve(result);
                })
                .catch((err) => {
                    clearTimeout(timer);
                    reject(err);
                });
        });
    };
}

// Example - 1
const limited = timeLimit((t) => new Promise(res => setTimeout(res, t)), 100);
limited(150).catch(console.log) // "Time Limit Exceeded" at t=100ms

// Example - 2
const fn = async (a, b) => { 
  await new Promise(res => setTimeout(res, 120)); 
  return a + b; 
}
const inputs = [5, 10];
const t = 150;

const limited = timeLimit(fn, t);
const start = performance.now();
let result;

try {
    const res = await limited(...inputs);
    result = {"resolved": res, "time": Math.floor(performance.now() - start)};
} catch (err) {
    result = {"rejected": err, "time": Math.floor(performance.now() - start)};
}

console.log(result); 
// Output: {"resolved":15,"time":120}


// Example - 3
const fn = async () => { 
  throw "Error";
}
const inputs = [];
const t = 1000;

const limited = timeLimit(fn, t);
const start = performance.now();
let result;

try {
    const res = await limited(...inputs);
    result = {"resolved": res, "time": Math.floor(performance.now() - start)};
} catch (err) {
    result = {"rejected": err, "time": Math.floor(performance.now() - start)};
}

console.log(result); 
// Output: {"rejected":"Error","time":0}






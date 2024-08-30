# Compact Object and Nested Array Generator

## Compact Object

### Problem Statement
Given an object or array `obj`, return a compact object. A compact object is the same as the original object, except with keys containing falsy values removed. This operation applies to the object and any nested objects. Arrays are considered objects where the indices are keys. A value is considered falsy when `Boolean(value)` returns `false`.

You may assume the `obj` is the output of `JSON.parse`. In other words, it is valid JSON.

### Example 1:
Input: obj = [null, 0, false, 1]
Output: [1]
Explanation: All falsy values have been removed from the array.

### Example 2:
Input: obj = {"a": null, "b": [false, 1]}
Output: {"b": [1]}
Explanation: obj["a"] and obj["b"][0] had falsy values and were removed.

### Example 3:
Input: obj = [null, 0, 5, [0], [false, 16]]
Output: [5, [], [16]]
Explanation: obj[0], obj[1], obj[3][0], and obj[4][0] were falsy and removed.

## Implementation

```javascript
/**
 * @param {Object|Array} obj
 * @return {Object|Array}
 */
var compactObject = function(obj) {
    if(Array.isArray(obj)){
     return obj
            .map(item => compactObject(item)) // Recursively compact each item in the array
            .filter(item => item); // Remove any falsy items
    }
    else if(typeof obj === 'object' && obj !== null){
      const result = {};
       for(let[key, value] of Object.entries(obj)){
         const compactedValue = compactObject(value); // Recursively compact the value
            if (compactedValue) {
                result[key] = compactedValue;
            }
       }
       return result;
    }
    return obj;
};


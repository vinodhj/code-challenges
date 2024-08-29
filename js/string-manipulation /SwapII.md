# SwapII Function

## Problem Statement

The `SwapII` function takes a string parameter and performs two transformations:
1. **Swap the case** of each character in the string.
2. If a letter is **sandwiched between two numbers** (with no spaces in between), swap the positions of the two numbers.

### Example

For example, if the input string is `"6Hello4 -8World, 7 yes3"`, the output should be `"4hELLO6 -8wORLD, 7 YES3"`.

## Solution

Here’s the JavaScript implementation of the `SwapII` function:

```javascript
function SwapII(str) {
    // Step 1: Swap the case of each character
    let swappedStr = str.split('').map(char => {
        if (char === char.toLowerCase()) {
            return char.toUpperCase();
        } else {
            return char.toLowerCase();
        }
    }).join('');

    // Step 2: Find and swap numbers that have a letter between them
    let result = swappedStr.replace(/(\d)([a-zA-Z]+)(\d)/g, (match, num1, letters, num2) => {
        return num2 + letters + num1;
    });

    return result;
}

// Test the function with the example input
console.log(SwapII("6Hello4 -8World, 7 yes3")); // Output: 4hELLO6 -8wORLD, 7 YES3

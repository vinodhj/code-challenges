# `generatePermutations` Function

## Description

The `generatePermutations` function generates all possible permutations of a given string. It uses recursion to explore all possible arrangements of the characters in the string.

## Function Definition

```javascript
function generatePermutations(str) {
    if(!isNaN(str)){
      str = str.toString();
    }
    if (str.length <= 1) return [str];
    let permutations = [];
    for (let i = 0; i < str.length; i++) {
        let char = str[i];
        let remainingChars = str.slice(0, i) + str.slice(i + 1);
        for (let permutation of generatePermutations(remainingChars)) {
            permutations.push(char + permutation);
        }
    }
    return permutations;
}

// Test the function with the example input
console.log(generatePermutations(910)); // Output: [ '910', '901', '190', '109', '091', '019' ]
console.log(generatePermutations(abc)); // Output:['abc', 'acb', 'bac', 'bca', 'cab', 'cba' ]]

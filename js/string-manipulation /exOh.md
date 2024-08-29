# Ex Oh

## Description

The `exOh` function determines if a given string contains the same number of 'x' characters as 'o' characters, ignoring case sensitivity.

### Input

- A string `str` consisting of any characters.

### Output

- Return `true` if the number of 'x' characters is equal to the number of 'o' characters in the string, ignoring case. Otherwise, return `false`.

## Function Definition

```javascript
function exOh(str) {
  // Convert the string to lowercase to handle case insensitivity
  const lowerStr = str.toLowerCase();
  
  // Count occurrences of 'x' and 'o'
  const countX = (lowerStr.match(/x/g) || []).length;
  const countO = (lowerStr.match(/o/g) || []).length;
  
  // Return true if counts are equal, otherwise false
  return countX === countO;
}

// Test cases
console.log(exOh("xo"));      // Output: true
console.log(exOh("xxoo"));    // Output: true
console.log(exOh("xoxo"));    // Output: true
console.log(exOh("xoxox"));   // Output: false
console.log(exOh("abc"));     // Output: true
```
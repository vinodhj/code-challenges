# Three Numbers

## Description

The `threeNumbers` function takes a string containing three integers separated by spaces. The function returns `true` if the first number is greater than the second, and the second is greater than the third. Otherwise, it returns `false`.

## Function Definition

```javascript
function threeNumbers(str) {
  // Split the input string into an array of numbers
  const [num1, num2, num3] = str.split(' ').map(Number);

  // Check if the numbers are in decreasing order
  return num1 > num2 && num2 > num3;
}

// Test cases
console.log(threeNumbers("10 5 1")); // Output: true
console.log(threeNumbers("1 5 10")); // Output: false
console.log(threeNumbers("5 5 5"));  // Output: false
console.log(threeNumbers("9 7 3"));  // Output: true

# Dash Insert

## Problem Description

The `dashInsert` function takes a number as input and returns a string where dashes (`-`) are inserted between each pair of consecutive odd digits in the number. The function avoids placing a dash at the end of the string and ensures that the dash is only inserted between valid consecutive digits.

## Implementation

The function iterates through the digits of the input number, checks each digit to see if it's odd, and if it finds consecutive odd digits, it inserts a dash between them, only if there is another digit after the current one.

## Function Definition

```javascript
function dashInsert(num) {
  if (isNaN(num)) {
    return null;
  }
  
  let str = num.toString();
  let num_dash = "";

  for (let i = 0; i < str.length; i++) {
    num_dash += str[i];
    if (str[i] % 2 !== 0 && str[i + 1] % 2 !== 0) {
      if (str[i + 1]) {
        num_dash += "-";
      }
    }
  }
  return num_dash;
}

console.log(dashInsert(454793)); // Output: "4547-9-3"
console.log(dashInsert(123456)); // Output: "123456"
console.log(dashInsert(1003567)); // Output: "1003-567"
console.log(dashInsert(13579)); // Output: "1-3-5-7-9"
console.log(dashInsert(2468)); // Output: "2468"
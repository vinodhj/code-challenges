# Basic Roman Numerals

## Description

The `romanToInt` function converts a string representing a basic Roman numeral into its corresponding integer value. This function handles Roman numerals using the standard notation and ensures correct conversion by considering both the additive and subtractive rules.

## Function Definition

```javascript
function romanToInt(roman) {
  const romanNumerals = {
    I: 1,
    V: 5,
    X: 10,
    L: 50,
    C: 100,
    D: 500,
    M: 1000
  };
  
  let total = 0;
  for (let i = 0; i < roman.length; i++) {
    const current = romanNumerals[roman[i]];
    const next = romanNumerals[roman[i + 1]];

    if (next && current < next) {
      total -= current;
    } else {
      total += current;
    }
  }
  return total;
}

console.log(romanToInt("III"));    // Output: 3
console.log(romanToInt("IV"));     // Output: 4
console.log(romanToInt("IX"));     // Output: 9
console.log(romanToInt("LVIII"));  // Output: 58
console.log(romanToInt("MCMXCIV"));// Output: 1994

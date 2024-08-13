# Vowel Count

## Description

The `vowelCount` function takes a string as input and returns the number of vowels (`a`, `e`, `i`, `o`, `u`) in the string. The function is case-insensitive, meaning it should count both uppercase and lowercase vowels.

## Function Definition

```javascript
function vowelCount(str) {
  // Initialize the count variable
  let vowel_tot_count = 0;
  
  // Convert string to lowercase, split it into an array of characters, and iterate over each character
  str.toLowerCase().split('').forEach(e => {
    // Check if the character is a vowel
    if (/[aeiou]/.test(e)) {
      vowel_tot_count++;
    }
  });
  
  // Return the total count of vowels
  return vowel_tot_count;
}

// Test cases
console.log(vowelCount("hello")); // Output: 2
console.log(vowelCount("HELLO")); // Output: 2
console.log(vowelCount("javascript")); // Output: 3
console.log(vowelCount("12345")); // Output: 0
console.log(vowelCount("")); // Output: 0
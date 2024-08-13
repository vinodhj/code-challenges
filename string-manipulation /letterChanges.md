# Letter Changes - JavaScript Solution

## Problem Statement

Write a function that takes a string and performs the following transformations:
1. Replace each letter in the string with the letter following it in the alphabet (i.e., 'a' becomes 'b', 'z' becomes 'a').
2. Capitalize every vowel in the new string (i.e., 'a', 'e', 'i', 'o', 'u').

Non-alphabetic characters should remain unchanged.

### Example

**Input:** `"hello world"`

**Output:** `"Ifmmp xpsmE"`

## Solution

Here is a simple implementation in JavaScript:

```javascript
function letterChanges(str) {
    // Convert the string to an array to manipulate each character
    let result = str.split('').map(char => {
        // Check if the character is a letter
        if (/[a-zA-Z]/.test(char)) {
            // Get the next character in the alphabet
            let nextChar = String.fromCharCode(char.charCodeAt(0) + 1);

            // If the character was 'z' or 'Z', wrap around to 'a' or 'A'
            if (char === 'z') nextChar = 'a';
            if (char === 'Z') nextChar = 'A';

            // Capitalize vowels
            if (/[aeiou]/.test(nextChar)) {
                nextChar = nextChar.toUpperCase();
            }

            return nextChar;
        } else {
            // If it's not a letter, return the character unchanged
            return char;
        }
    });

    // Join the array back into a string
    return result.join('');
}

// Test the function
console.log(letterChanges("hello world")); // Output: "Ifmmp xpsmE"

# Simple Symbols

## Description

The `simpleSymbols` function checks if each alphabetic character in a given string is surrounded by a `+` symbol on both sides. If every letter is properly surrounded, the function returns `true`; otherwise, it returns `false`.

## Function Definition

```javascript
function simpleSymbols(str) {
    // Loop through the string to check each character
    for (let i = 0; i < str.length; i++) {
        let char = str[i];

        // Check if the character is a letter
        if (/[a-zA-Z]/.test(char)) {
            // Check if the letter is not surrounded by '+' on both sides
            if (i === 0 || i === str.length - 1 || str[i - 1] !== '+' || str[i + 1] !== '+') {
                return false;
            }
        }
    }
    // If all letters are properly surrounded, return true
    return true;
}


console.log(simpleSymbols("+d+===+c+++")); // true
console.log(simpleSymbols("f++d+"));  // false

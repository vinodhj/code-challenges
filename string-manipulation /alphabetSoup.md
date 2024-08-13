# Alphabet Soup

## Description

The `alphabetSoup` function takes a string as input and returns a new string where all the characters are sorted in alphabetical order. This is useful for simple string manipulations where you need to rearrange the characters of a string.

## Function Definition

```javascript
function alphabetSoup(str) {
    // Split the string into an array of characters, sort them, and join them back into a string
    return str.split('').sort().join('');
}

console.log(alphabetSoup("vinodh")); // Output: "dhinov"
console.log(alphabetSoup("hello"));     // Output: "ehllo"
console.log(alphabetSoup("javascript"));// Output: "aacijprstv"
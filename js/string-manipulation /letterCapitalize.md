# Letter Capitalize

## Description

The `letterCapitalize` function takes a string as input and returns the string with the first letter of each word capitalized. Words in the string are assumed to be separated by spaces.

## Function Definition

```javascript
function letterCapitalize(str) {
    return str.split(' ')
        .map(word => word.charAt(0).toUpperCase() + word.slice(1))
        .join(' ');
}

console.log(letterCapitalize("hello world")); // "Hello World"
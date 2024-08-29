# Distinct Characters

## Description

The `hasDistinctCharacters` function checks if a string contains only distinct characters. It returns `true` if all characters in the string are unique, and `false` otherwise.

## Function Definition

## Solution - 1

```javascript
function hasDistinctCharacters(str) {
  const charSet = new Set(str);
  return charSet.size === str.length;
}
```

## Solution - 2 [Using the `reduce` method and an object to track character counts]

```javascript
function hasDistinctCharacters(str) {
  const charCount = str.split("").reduce((acc, curr) => {
    acc[curr] = (acc[curr] || 0) + 1;
    return acc;
  }, {});

  for (let value of Object.values(charCount)) {
    if (value > 1) {
      return false;
    }
  }
  return true;
}

// Test cases
console.log(hasDistinctCharacters("abcdef")); // Output: true
console.log(hasDistinctCharacters("aabbcc")); // Output: false
console.log(hasDistinctCharacters("123456")); // Output: true
console.log(hasDistinctCharacters("a1b2c3")); // Output: true
console.log(hasDistinctCharacters("hello")); // Output: false
```

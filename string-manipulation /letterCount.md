# Letter Count I

This document provides a solution to the "Letter Count I" problem, which involves counting the occurrences of each letter in a string and determining the letter with the highest count.

## Problem Description

Given a string, count the number of occurrences of each letter and return the letter with the highest count. If there are multiple letters with the highest count, return the one that appears first in the string.

## JavaScript Solution

The following JavaScript function counts the occurrences of each letter in a string and returns the letter with the highest count:

```javascript
function letterCount(str) {
  const str_reduce = str
    .toLowerCase()
    .split("")
    .reduce((acc, curr) => {
      acc[curr] = (acc[curr] || 0) + 1;
      return acc;
    }, {});
  
  let maxCount = 0;
  let maxLetter = "";

  for (const [key, value] of Object.entries(str_reduce)) {
    if (value > maxCount) {
      maxCount = value;
      maxLetter = key;
    }
  }

  return maxLetter;
}

// Example usage
const str = "abacabad";
console.log(letterCount(str)); // Output: 'a'

# RepeatWord Function

This document describes the `repeatWord` function, a JavaScript function designed to process a string where each character is followed by a number. The function expands each character in the string based on the number that follows it.

## Problem Statement

Given a string where each character is followed by a number, expand the character according to the number of times specified. For example:

- Input: `"a1b10"`
- Output: `"abbbbbbbbbb"`

## Implementation

Here is the JavaScript implementation of the `repeatWord` function:

```javascript
function repeatWord(str) {
  let temp_word = "";
  let temp_num = "";
  let result = [];
  
  str.split("").forEach((e, index, str_arr) => {
    if (isNaN(e)) {
      temp_word = e;
    } else {
      temp_num += e;
      if (isNaN(str_arr[index + 1]) || index === str_arr.length - 1) {
        const temp_array = new Array(Number(temp_num)).fill(temp_word);
        result.push(...temp_array);
        temp_word = "";
        temp_num = "";
      }
    }
  });
  
  return result.join("");
}

// Example usage
console.log(repeatWord("a1b10"));  // Output: "abbbbbbbbbb"
console.log(repeatWord("b3c6d15")); // Output: "bbbccccccddddddddddddddd"

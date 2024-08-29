# Alphabet Searching

## Description

The `alphabetSearching` function checks if a given string contains every letter of the alphabet at least once. It is case-insensitive and ignores non-alphabetic characters. If the string contains all the letters, the function returns `true`; otherwise, it returns `false`.

## Function Definition

```javascript
function alphabetSearching(str) {
  const alphabet = new Set("abcdefghijklmnopqrstuvwxyz");

  for (let char of str.toLowerCase()) {
    if (/[a-z]/.test(char)) {
      alphabet.delete(char);
      if (alphabet.size === 0) {
        return true;
      }
    }
  }
  return alphabet.size === 0;
}

// Test cases
console.log(alphabetSearching("The quick brown fox jumps over the lazy dog")); // Output: true
console.log(alphabetSearching("Hello World!")); // Output: false
console.log(alphabetSearching("ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz")); // Output: true
console.log(alphabetSearching("Sphinx of black quartz, judge my vow!")); // Output: true
console.log(alphabetSearching("This is just a random sentence.")); // Output: false

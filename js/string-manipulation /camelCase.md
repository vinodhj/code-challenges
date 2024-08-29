# Camel Case

## Description

The `camelCase` function converts a string into CamelCase format. In CamelCase, the first word is in lowercase, and each subsequent word starts with an uppercase letter, with all spaces removed.

## Solution - 1
```javascript
function camelCase(str) {
  const result = str.split(" ").map((e, index) => {
    const first_char = e.slice(0, 1);
    const remaining_char = e.slice(1);
    if (index === 0) {
      return first_char.toLowerCase() + remaining_char.toLowerCase();
    }
    return first_char.toUpperCase() + remaining_char.toLowerCase();
  });
  return result.join("");
}
```

## Solution - 2 [Using Regex]
```javascript
/**
 * (?:...): Non-Capturing Groups eg: (?:cat|dog)s? -> Matches cat, dogs, dog, or cats. The non-capturing group (?:cat|dog) allows for matching either cat or dog, and the s? makes the trailing s optional.
 *  /^\\w: Matches the very first word character of the string
 * [A-Z]: Matches any uppercase letter in the string.
 * \\b\\w: Matches the beginning of any word after a word boundary.
 * \\s+: Matches sequences of whitespace characters.
 */
function camelCase(str) {
  return str
    .toLowerCase()
    .replace(/(?:^\w|[A-Z]|\b\w|\s+)/g, (match, index) => 
      index === 0 ? match.toLowerCase() : match.toUpperCase().replace(/\s+/g, '')
    );
}

// Test cases
console.log(camelCase("hello world")); // Output: "helloWorld"
console.log(camelCase("Camel Case Conversion")); // Output: "camelCaseConversion"
console.log(camelCase("javaScript is fun")); // Output: "javaScriptIsFun"
console.log(camelCase("convert to camel case")); // Output: "convertToCamelCase"
console.log(camelCase("")); // Output: ""

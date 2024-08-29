# TimeLimitedCache Implementation Comparison

This document compares two different approaches to implementing a `TimeLimitedCache` class, which allows setting and getting key-value pairs with a time limit for expiration.

## Overview

The `TimeLimitedCache` class has three main methods:

1. **`set(key, value, duration)`**: Stores a key-value pair with a time-to-live (TTL) specified by `duration` in milliseconds.
2. **`get(key)`**: Retrieves the value associated with a key if it hasn't expired; otherwise, returns `-1`.
3. **`count()`**: Returns the count of currently unexpired keys.

## Approach 1: Using Expiry Time with `Date.now()`

### Implementation - 1

```javascript
const TimeLimitedCache = function () {
    this.cache = new Map();
};

TimeLimitedCache.prototype.set = function (key, value, duration) {
    const currentTime = Date.now();
    const existingEntry = this.cache.get(key);
    const isExistingUnexpiredKey = existingEntry && (existingEntry.expiryTime > currentTime);

    if (isExistingUnexpiredKey) {
        clearTimeout(existingEntry.timeoutId);
    }

    const timeoutId = setTimeout(() => {
        this.cache.delete(key);
    }, duration);

    this.cache.set(key, {
        value: value,
        expiryTime: currentTime + duration,
        timeoutId: timeoutId
    });

    return isExistingUnexpiredKey;
};

TimeLimitedCache.prototype.get = function (key) {
    const currentTime = Date.now();
    const entry = this.cache.get(key);

    if (entry && entry.expiryTime > currentTime) {
        return entry.value;
    }

    return -1;
};

TimeLimitedCache.prototype.count = function () {
    const currentTime = Date.now();
    let activeKeys = 0;

    for (let entry of this.cache.values()) {
        if (entry.expiryTime > currentTime) {
            activeKeys++;
        }
    }

    return activeKeys;
};
```

## Approach 2: Using setTimeout with Immediate Deletion on Expiration

### Implementation - 2

```javascript
const TimeLimitedCache = function() {
    this.cache = new Map();  // Using Map so we don't need a size variable
};

TimeLimitedCache.prototype.set = function(key, value, duration) {
    let found = this.cache.has(key);
    if (found) clearTimeout(this.cache.get(key).ref);  // Cancel previous timeout
    this.cache.set(key, {
        value,  // Equivalent to `value: value`
        ref: setTimeout(() => this.cache.delete(key), duration)
    });
    return found;
};

TimeLimitedCache.prototype.get = function(key) {
    return this.cache.has(key) ? this.cache.get(key).value : -1;
};

TimeLimitedCache.prototype.count = function() {
    return this.cache.size;
};

// Input:
["TimeLimitedCache", "set", "get", "count", "get"]
[[], [1, 42, 100], [1], [], [1]]
[0, 0, 50, 50, 150]

// Output:
[null, false, 42, 1, -1]

/**
 * Example Usage:
 * const timeLimitedCache = new TimeLimitedCache();
 * console.log(timeLimitedCache.set(1, 42, 1000)); // Output: false
 * console.log(timeLimitedCache.get(1)); // Output: 42
 * console.log(timeLimitedCache.count()); // Output: 1
 */
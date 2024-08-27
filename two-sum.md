# Two Sum

## Problem Description

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1
**Input:** `nums = [2, 7, 11, 15]`, `target = 9`  
**Output:** `[0, 1]`  
**Explanation:** Because `nums[0] + nums[1] == 9`, we return `[0, 1]`.

### Example 2
**Input:** `nums = [3, 2, 4]`, `target = 6`  
**Output:** `[1, 2]`  
**Explanation:** Because `nums[1] + nums[2] == 6`, we return `[1, 2]`.

### Example 3
**Input:** `nums = [3, 3]`, `target = 6`  
**Output:** `[0, 1]`  
**Explanation:** Because `nums[0] + nums[1] == 6`, we return `[0, 1]`.

## Solution 1: Brute-Force Approach

### Description

The brute-force approach involves checking all possible pairs of indices to find the pair that adds up to the `target`. This method uses two nested loops to iterate through the array.

### Implementation - 1
```javascript
var twoSum = function (nums, target) {
    for (let i = 0; i < nums.length; i++) {
        const current_index = i;
        for (let j = 0; j < nums.length; j++) {
            // Ignore current_index
            if (j === current_index) {
                continue;
            }
            if (nums[j] + nums[current_index] === target) {
                return [i, j];
            }
        }
    }
};

### Implementation - 2
var twoSum = function(nums, target) {
    const map = new Map(); // Create a map to store the indices of the elements

    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i]; // Calculate the complement of the current number
        
        // Check if the complement exists in the map
        if (map.has(complement)) {
            return [map.get(complement), i]; // Return the indices of the complement and current number
        }
        
        // Store the index of the current number in the map
        map.set(nums[i], i);
    }
};

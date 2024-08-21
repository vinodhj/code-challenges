# Explanation of `sortColors` Function in JavaScript

The `sortColors` function is designed to sort an array of numbers in place, specifically handling an array that contains only the numbers `0`, `1`, and `2`. This is commonly known as the Dutch National Flag problem.


## How It Works

### 1. **In-Place Array Modification**
   - **Pass by Reference:** In JavaScript, arrays (and objects) are passed to functions by reference. This means that when you pass an array to a function, the function operates on the actual array in memory, not a copy of it.
   - **No Return Needed:** Since the function modifies the original array directly, there’s no need for it to return a new array. The original array will be updated after the function executes.

### 2. **The Algorithm**
   - **Initialization:**
     - `low`, `mid`: Start at the beginning of the array.
     - `high`: Starts at the end of the array.
   - **Sorting Logic:**
     - **When `nums[mid]` is `0`:**
       - Swap `nums[mid]` with `nums[low]`.
       - Increment both `low` and `mid`.
     - **When `nums[mid]` is `1`:**
       - Simply move the `mid` pointer forward.
     - **When `nums[mid]` is `2`:**
       - Swap `nums[mid]` with `nums[high]`.
       - Decrement `high`.

### 3. **Example**

```javascript
const sortColors = function (nums) {
  let low = 0,
    mid = 0,
    high = nums.length - 1;
  while (mid <= high) {
    if (nums[mid] === 0) {
      [nums[low], nums[mid]] = [nums[mid], nums[low]];
      low++;
      mid++;
    } else if (nums[mid] === 1) {
      mid++;
    } else {
      [nums[mid], nums[high]] = [nums[high], nums[mid]];
      high--;
    }
  }
};

let nums = [2, 0, 2, 1, 1, 0];
sortColors(nums);
console.log(nums); // Output: [0, 0, 1, 1, 2, 2]

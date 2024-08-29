# Calculator with Method Chaining

This document explains the implementation of a custom `Calculator` class that supports method chaining for performing basic arithmetic operations. The class allows users to chain multiple operations together and retrieve the final result.

## Implementation

The `Calculator` class provides methods for addition, subtraction, multiplication, division, and exponentiation. Each method returns the `Calculator` instance to allow chaining. The class also provides a method to retrieve the current result.

### Code

```javascript
class Calculator {
    /** 
     * @param {number} value - The initial value of the calculator.
     */
    constructor(value) {
        this.result = value;
    }
    
    /** 
     * Adds the given value to the current result.
     * @param {number} value - The number to add.
     * @return {Calculator} The calculator instance for chaining.
     */
    add(value){
        this.result += value;
        return this;
    }
    
    /** 
     * Subtracts the given value from the current result.
     * @param {number} value - The number to subtract.
     * @return {Calculator} The calculator instance for chaining.
     */
    subtract(value){
         this.result -= value;
         return this;
    }
    
    /** 
     * Multiplies the current result by the given value.
     * @param {number} value - The number to multiply by.
     * @return {Calculator} The calculator instance for chaining.
     */  
    multiply(value) {
        this.result *= value;
        return this;
    }
    
    /** 
     * Divides the current result by the given value.
     * @param {number} value - The number to divide by.
     * @return {Calculator} The calculator instance for chaining.
     * @throws {Error} If the value is zero, throws an error.
     */
    divide(value) {
        if(value === 0){
            this.result =  "Division by zero is not allowed";
            return this;
        }
        this.result /= value;
        return this;
    }
    
    /** 
     * Raises the current result to the power of the given value.
     * @param {number} value - The exponent to raise the result to.
     * @return {Calculator} The calculator instance for chaining.
     */
    power(value) {
        this.result **= value;
        return this;
    }
    
    /** 
     * Returns the current result.
     * @return {number} The current result.
     */
    getResult() {
        return this.result;
    }
}


// Initialize the calculator with a starting value of 10
const calculator = new Calculator(10);

// Perform a series of operations
const result = calculator
    .add(5)           // 10 + 5 = 15
    .subtract(3)      // 15 - 3 = 12
    .multiply(4)      // 12 * 4 = 48
    .divide(2)        // 48 / 2 = 24
    .power(3)         // 24 ^ 3 = 13824
    .getResult();     // Retrieve the final result

console.log(result); // Output: 13824

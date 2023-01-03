## Types
### Primitive Types:
- undefined
- string
- number
- boolean
- object
- symbol
- null
- bigint
##
- undeclared ? 
- function ? Sub-type of the object type.
- array ? Sub-type of the object type.

    ```javascript
    var v = null
    typeof v        // "object"

    v = function(){}
    typeof v        // "function"

    v = [1, 2, 3]
    typeof v        // "object"
    ```

 > If you wanted to unset a regular value like a number you should use **undefined** but if you want to unset a refrence object you should use **null**. And that's somehow why typeof null returns "object" but he thinks that is a bug!

##### ===
-  **NaN**
    -  Not a valid number. 
    - Look for OOPS xD

        ```javascript
        var myAge = Number("0o46")      // 38
        var myNextAge = Number("39")    // 39
        var myCatsAge = Number("n/a")   // NaN
        myAge = "my son's age"

        myCatsAge === myCatsAge         // false OOPS!
        // NaN is the only value that does not have the identity property meaning that its not equal to itself!

        isNaN(myAge)            // false
        isNaN(myCatsAge)        // true
        isNaN("my son's age")   // true OOPS!
        // The isNaN utitility coercive values to numbers before checking if they're NaN!

        // They've fixed this with ES6
        Number.isNaN(myCatsAge)         // true
        Number.isNaN("my son's age")    // false

        // NaN reutrns false comparing it to itslef and this happens only with NaN in JS.
        function isItNaN(value) {
            return value !== value
        }
        ```
###### ===
-  **Negative Zero**
```javascript
var trendRate = -0
trendRate === -0        // true

trendRate.toString()    // "0"  OOPS!
trendRate === 0         // true OOPS!
trendRate < 0           // false
trendRate > 0           // false
// JS developers in the past were trying to guess the bugs and fix them themselves!

// To solve that
Object.is(trendRate, -0)    // true
Object.is(trendRate, 0)     // false
```

---

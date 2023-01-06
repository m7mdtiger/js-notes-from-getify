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
### Coercion
- Coercion means type conversion.

- toNumber()
```javascript
toNumber("")    // 0
toNumber("0")    // 0
toNumber("-0")    // -0
toNumber(" 009 ")    // 009
toNumber("3.14159")    // 3.14159
toNumber("0.")    // 0
toNumber(".0")    // 0
toNumber(".")    // NaN
toNumber("0xaf")    // 175
toNumber(true)    // 1
toNumber(false)    // 0
toNumber(null)    // 0
toNumber(undefined)    // NaN
```
 ===
 - toBoolean(): returns false only if the value is one of these values without doing any coercion..
    - ""
    - 0, -0
    - null
    - NaN
    - false
    - undefined
> Note that empty strings return 0

### Cases of Coercion
- When using template strings, you're using coercion.
```javascript
var num = 12
console.log(`Number = ${num}`)
```

### Corner Cases of Coercion
```javascript
Number("")              // 0
Number("    \t\n")      // 0
Number(null)            // 0
Number(undefined)       // NaN
Number([])              // 0
Number([1, 2, 3])       // NaN
Number([null])          // 0
Number(undefined)       // 0
Number({})              // NaN

String(-0)              // "0"
String(null)            // "null"
String(undefined)       // "undefined"
String([null])          // ""
String([undefined])     // ""

Boolean(new Boolean(false)) // true
```

> People write **comments** about **how** and they forget about **why**

### Equality
```javascript
+0 === -0   // true
NaN === NaN // false

null == undefined // true
```

- == algorithm summary
    - If types are the same use ===
    - null or undefined are equal.
    - Non primitives will be coerced using toPrimitive()
    - Uses toNumber() for coercion.

- Avoid:
    1. == with 0 or "" (or even "  ")
    2. == with non-primitives
    3. == true or == false
    4. using == when you don't know the types


---
### Scope & Expressions
> If not in "use strict" mode, **undeclared** won't be an error.

- You should prefer the named function expression over the anonymouns function expression
    1. Reliable function self-reference (recursion, etc).
    2. More debuggable stack traces.
    3. More self-documenting code.

---
### Closure
> **lexical scope** refers to it's current surrounding scope and no further.

> **Closure** is when a function 'remembers' its lexical scope even when the function is executed outside that lexical scope.

```javascript
// Note: Closure capture variables not values
// The following prints i:4, 3 times    // OOPS!
for (var i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(`i: ${i}`)
    }, i * 1000)
}

// You can use let instead of var to capture the values
// The following prints i:1, i:2 & i:3
for (let i = 1; i <= 3; i++) {
    setTimeout(function() {
        console.log(`i: ${i}`)
    }, i * 1000)
}

// If you wanna keep using var, then assign i to a variable usig let
for (var i = 1; i <= 3; i++) {
    let j = i
    setTimeout(function() {
        console.log(`j: ${j}`)
    }, j * 1000)
}
```


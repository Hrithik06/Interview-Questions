## 1. console.log([]+{}) 
### Answer = [object Object]

### Explanation
This happens due to JavaScript's type coercion rules when using the + operator with non-primitive types like arrays and objects:

[] is an empty array, which when coerced to a primitive for concatenation, becomes an empty string "".

{} is an empty object, which when coerced to a primitive (string context), becomes the string "[object Object]".

So the expression [] + {} is effectively:

```js
"" + "[object Object]"
```
which results in the string:

"[object Object]"

This string is then logged to the console by console.log().

### Additional Notes:

The + operator in JavaScript, when used with objects, tries to convert them to primitives. For arrays, this usually means calling .toString() which joins elements with commas (empty array becomes an empty string).
For plain objects, the default .toString() returns "[object Object]".
This behavior is consistent across browsers and JavaScript engines.

### Summary
#### Expression	Result	Reason
[]	"" (empty string)	Array coerces to empty string\
{}	"[object Object]"	Object coerces to string representation\
[] + {}	"[object Object]"	Concatenation of "" + "[object Object]"\

Therefore, console.log([] + {}) outputs:

**[object Object]**

This is a common JavaScript quirk related to type coercion and operator overloading with objects and arrays.

No additional parameters or special console features affect this output; it's purely how JavaScript evaluates the expression before logging it.

## 2. Number("123Abc")
### Answer = NaN
1. Number("123Abc")

    Here, "123Abc" is a string containing digits followed by letters.

    The Number() function tries to convert the entire string to a number.

    Since "123Abc" is not a valid numeric string (due to the letters Abc), the conversion fails.

    The result is NaN (Not a Number).

    ```js
    console.log(Number("123Abc")); // Output: NaN
    ```
2. Number(123Abc)

    This is invalid JavaScript syntax.

    123Abc is not a valid number or variable name.

    JavaScript interprets this as a numeric literal 123 immediately followed by an identifier Abc without any operator or separator, which causes a syntax error.

    If you try to run:

    ```js
    console.log(Number(123Abc));
    ```
    You will get a ReferenceError or SyntaxError

    Uncaught SyntaxError: Unexpected identifier
   
## 3. string.slice(1) removes first character
The slice() method extracts a section of a string and returns it as a new string, without modifying the original string

When you use slice(1), you are telling JavaScript to start extracting from index 1 (the second character) and continue to the end of the string.

Indexing in JavaScript strings starts at 0, so index 1 skips the first character

Example:
```js
const str = "Hello";
console.log(str.slice(1)); // Output: "ello"
```

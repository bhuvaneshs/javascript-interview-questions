# javascript-interview-questions
Javascript Interview Questions

1) what is closure? Explain the real world scenario? 

A closure is an inner function that has access to its lexical scopes which includes it's own scope, parent scope and the global scope.

or 

A closure is a function that remembers the variable from its outer function even after the outer function has finished execution.

Definition 1 Example:

let firstName = "Alice"; // global scope

function parent(){
  let lastName = "bob"; // parent scope
  return function child(){
    let middleName = "John"; // child scope
	console.log(firstName,lastName,middleName);
  }
}

const fnCall = parent();
fnCall();

Definition 2 Example:

function counter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const increment = counter();
increment(); // 1
increment(); // 2
increment(); // 3

Real world Example : Dynamic Field Validator (Reusability via Closure) : 
function createValidator(fieldName) {
  return function (value) {
    if (!value) {
      return `${fieldName} is required`;
    }
    if (fieldName === 'Email' && !value.includes('@')) {
      return 'Please enter a valid email';
    }
    return `${fieldName} looks good!`;
  };
}

// Create specific validators using closures
const validateEmail = createValidator('Email');
const validatePassword = createValidator('Password');

// Usage
console.log(validateEmail(""));             // "Email is required"
console.log(validateEmail("testexample"));  // "Please enter a valid email"
console.log(validatePassword("12345")); 

2) what is the purpose of "use strict" in Javascript?

use strict is a directive that enforces strict parsing and error handling in javascript code 

'use strict'; makes your code less error-prone, easier to debug, and more secure by eliminating some silent bugs and enforcing better practices.

Examples :
1) Prevents accidental globals
   
'use strict';
x = 10; // ❌ ReferenceError: x is not defined

3) Disallows duplicate parameter names
   
'use strict';
function test(a, a) {} // ❌ SyntaxError

5) Disallows assignment to read-only or non-writable properties
   
'use strict';
const obj = {};
Object.defineProperty(obj, "x", { value: 42, writable: false });
obj.x = 9; // ❌ TypeError

7) Makes this undefined in functions (not the global object)
   
'use strict';
function show() {
  console.log(this); // ❌ undefined (instead of window/global)
}
show();

9) Throws errors for using reserved keywords for future JS versions

'use strict';
let public = 123; // ❌ SyntaxError

Note: we can able to use strict mode inside the function block too.

Ex: 
function getName(firstName,lastName){
  "use strict"
  return firstName+" "+lastName;
}

3) what is higher-order function? why we need to use it?

A Higher-Order Function in JavaScript is a function that does at least one of the following:

a) Takes another function as an argument (callback function).

b) Returns another function.

Some of the built-in higher order functions are map, filter and reduce.

Example 1: (function taking another function as an argument)

function greet(name, callback) {
    console.log("Hello, " + name);
    callback();
}

function sayGoodbye() {
    console.log("Goodbye!");
}

greet("Alice", sayGoodbye);

Example 2: Function Returning Another Function

function multiplyBy(factor) {
    return function (number) {
        return number * factor;
    };
}

const double = multiplyBy(2);
console.log(double(5)); // Output: 10

Example 3: Using Built-in Higher-Order Functions (map, filter, reduce)

#Using map to modify array values
const numbers = [1, 2, 3, 4];
const squared = numbers.map(num => num * num);
console.log(squared); // Output: [1, 4, 9, 16]

#Using filter to get even numbers
const evenNumbers = numbers.filter(num => num % 2 === 0);

#Using reduce to sum up numbers
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // Output: 10

In the above example map,filter and reduce takes another function as an argument.
console.log(evenNumbers); // Output: [2, 4]

Purpose:-

a) They make code more reusable and modular.

b) They improve readability and maintainability.

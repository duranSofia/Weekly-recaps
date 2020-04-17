## week-14-recap

this short week is mostly project time, but we did some cool recaps.
Firstly, with Javascript.

**Data types**:

they can be primitives:

string: "hello"
number: 1,2,3
Boolean: true, false
Null: null
symbol: \* + #
BigInt: 10n

Their value is immuntable! So they cannot be changed.

The typeOf method can be fun to play with.

`typeof(10) "number" typeof(true) "boolean" typeof(undefined) "undefined"`

all good with these. but:

``
typeof(null)
"object"

``
Null is an object that is a bug. And it cannot be fixed because it would break the existing codebase, and it would break millions of websites...

**Non-primitives**

Function: function hello();
Object: {};
Array: ["apple", "orange", "banana"]

Non-primitives values are mutable, they can be changed after its creation!

`typeof([1,2,3]); "object"`

Arrays are objects!

``
typeof(typeof(42));
"number"- that is a "string"

typeof(“undefined”);
Uncaught SyntaxError: Invalid or unexpected token

typeof(value)
"undefined"
``

Some interview questions:

`// Question: What is the value of foo.length? var foo = []; foo.push(1); foo.push(2); 2`

``
What will be logged and why
let reaction = 'yikes';
reaction[0] = 'l';
console.log(reaction);


Fibonacci:

Given a number N return the index value of the Fibonacci sequence, where the sequence is:
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...

each value is the sum of the 2 previous values- wich in maths is written like this:

f(n) = f(n-1) + f(n-2)

 and in JS:

```
function fibonacci(num){
let arr = [0, 1];
function fib(n){
let arr = [0, 1];
for (let i = 2; i < n + 1; i++){
arr.push(arr[i - 2] + arr[i -1])
}
return arr[n]
}


console.log(fib(10));

55

```



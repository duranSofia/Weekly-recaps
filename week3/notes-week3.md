### week3-recap
We dived very deep into Javascript and we started React :)

### Test Driven Development
We started with an Odyssey quest about TDD (Test Driven Development). Here we had our first contact with Node- with had to fork clone a repository with various Javascript data types: "primitive" types (numbers, strings, booleans and the "undefined" type), arrays, objects and functions. Here we had to run the test program, see it fail, and then make it pass with writing passing code to the test result.

### Javascript ES6
ECMAScript 6 is also known as ES6 and ECMAScript 2015.

Some new features were introduced then. For example, the variable names changed from var to:

1. let- if we want to change them
2. const- if we do not want to change them
Other important features:

Arrow Functions:
```
hello = () => {
  return "Hello World!";
}

Ternary operator

Instead of "if else" statements, we can use just use: ?

const name = "Leo";
console.log (name === "Leo" ? "Welcome Leo!" : "Go away!");
Methods with arrays
Some very useful functions that can be used with arrays, and they make our life with Javascript easier.

Filter: it filters out, and creates a new array from the array's elements:

let number = [4,12,23];
let moreThanFive = numbers.filter(element => element > 5);
cosole.log(moreThanFive); // 12, 23
Map:

method creates a new array with the results of calling a function for every array element.

const people = [
  { name: "James", age: 18 },
  { name: "Alice", age: 20 }
];

const names = people.map(element => element.name);
console.log(names); // "James", "Alice". 
forEach Similar to the for loop, but not only loops through the array, but it executes a provided function once for each array element:

const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
find it finds a specific element of the array:

[const people = [
  { name: "James", age: 18 },
  { name: "Alice", age: 20 },
  { name: "John", age: 17 },
  { name: "Maria", age: 65 },
  { name: "James", age: 65 }
];
const found = people.find(
  element => element.age === 65 && element.name === "James"
);
console.log(found); // [James, 65];]
math.random

Return a random number between 0 (inclusive) and 1 (exclusive):


[Math.floor((Math.random() * 10) + 1); ]
reduce

The array reduce() method in JavaScript is used to reduce the array to a single value and executes a provided function for each value of the array (from left-to-right) and the return value of the function is stored in an accumulator.

[const euros = [29.76, 41.85, 46.5];

const sum = euros.reduce((total, amount) => total + amount); 

sum // 118.11]
In this example, reduce accepts two parameters, the total and the current amount. The reduce method cycles through each number in the array much like it would in a for-loop. When the loop starts the total value is the number on the far left (29.76) and the current amount is the one next to it (41.85). In this particular example, we want to add the current amount to the total. The calculation is repeated for each amount in the array, but each time the current value changes to the next number in the array, moving right. When there are no more numbers left in the array the method returns the total value.

Object Oriented Programming
In this concept we create "blueprints": consctructors and classes and we can reuse again the code:

`class Vehicle {
  constructor(color, model, type) {
    this.color = color;
    this.model = model;
    this.type = type;
  }
  }
the classes can have methods:

display() {
  return `${this.type}: ${this.color}: ${this.model}: `;
}
we can create new instances, just by using the "new" word:

const vehicle = new Vehicle("blue", "VW Beetle", "car");
console.log(vehicle.display());
Inheritance: a new class that extends from the parent class vehicle:

class Car extends Vehicle {

 constructor(color, model) {
    super(color, model, "car"); //the type will always be car, it is already predefined
  }
}

we can also override the parent's method:

lock() {
    return `Your ${this.color} ${this.model} is now locked!`;
  }
  display() {
    return `We can override the parent's method!`; //new method added, we can add as many methods as we want
  }
Agile Methodology and SCRUM
A team of smart people went to the mountains in the US in 2001, and they created a manifesto (method) that makes software development more organised and visible.

The Three Pillars of SCRUM

Transparency: Giving visibility to significant aspects of the process to those responsible for the outcome.

Inspection: Timely checks on the progress toward a sprint goal to detect undesirable variances.

Adaption: Adjusting a process as soon as possible to minimize any further deviation or issues.

SCRUM ROLES

Product Owner: Represents the client and the business in general for the product they are working.
SCRUM Master : Ensures that the team has everything they need and they deliver value (get shit done).
Development Team: a group of cross-functional people who work on delivery of the working software.
SPRINT

A process of 1 months that the team delivers a working software from scratch. Then it has a development cicle- so it is constantly tested and improved. MVP = Minimum Viable Product

SCRUM is divided into 4 ceremonies

Sprint planning
Daily meeting
Review
Retrospective
Sprint Backlog Done with the product owner: the tasks are categorised acccording to the complexity.

Product Backlog- User story The product's features are told step-by-step from the user's perspective. Specific formula:

As a < type of user >, I want < some goal > so that < some reason >.

Daily standups

Maximum 15 minutes

What we did the day before
What we plan to do
Blocking points
The mood
Review Demo in the front of the client to show the progress and get feedback.

Retrospective What went well, what not, how can we progress.

## week-14-recap

this short week is mostly project time, but we did some cool recaps.
Firstly, with Javascript.

**Data types**:

they can be primitives:

string: "hello"
number: 1,2,3
Boolean: true, false
Null: null
symbol: symbol(‘hello’)
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

typeof(undefined);
"undefined"

``

Some interview questions:


```
What will be logged and why
let reaction = 'yikes';
reaction[0] = 'l';
console.log(reaction);
yikes
```

Fibonacci:

Given a number N return the index value of the Fibonacci sequence, where the sequence is:
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...

each value is the sum of the 2 previous values- wich in maths is written like this:

f(n) = f(n-1) + f(n-2)

 and in JS:


```

function fibonacci(num){
let arr = [0, 1];
for (let i = 2; i < n + 1; i++){
arr.push(arr[i - 2] + arr[i -1])
}
return arr[n]
}
console.log(fib(10));

55

```

```

## Object-oriented programming (OOP)
A programming paradigm - a way, a style you program - for structuring complex code.
Objects: abstractions that represent real word things in the program (- abstractions).

**How to create an object?**

    const wilder1 = createObject();
    wilder1.firstName = "Marc";
    wilder1.campus: "Berlin";
    wilder1.sayHello: function(){
		return  `hello my name is ${wilder1.firstName}`
	}
Or:

    const wilder1 = {
	    firstName: "Marc",
	    campus: "Berlin",
	    sayHello: function(){
		    return  `hello my name is ${wilder1.firstName}`
		}
	};

**"Object-factory"**

    function createWilder(firstName, lastName, city) 
    {
	    const wilder = {}
	    wilder.firstName = firstName;
	    wilder.city = city,
	    wilder.sayHello = function(){
		    return  `hello I'm ${wilder.firstName}`
		    }
	};
	
	const wilder1 = createWilder('Mia', 'Berlin');
	wilder1.sayHello();

 - problem: we are re-creating the sayHello function again, and again, and again with every new wilder.



**Functions in JS**

"Special objects" = function and Object at the same time.

    function sth() {
	    return "Hello"
	}
	sth.number = 18;
	
	> sth();
		"Hello"
	> sth.number;
		18

**&lowbar;&lowbar;proto&lowbar;&lowbar;** is internal property of an object, pointing to its prototype. (A portal to reach prototype.) => **prototype** is a place where "hidden functions" inherited from the parent can be stored.

![example of __proto__ and prototype](https://i.imgur.com/O2yvM4c.jpg)

Using prototype to avoid re-creation of function every time when a new wilder are created:

    function createWilder(firstName, city) {
	    const wilder = Object.create(wilderActions);
		    // Object.create() creates a new object, using an existing object as the prototype of the newly created object.
		wilder.firstName = firstName,
		wilder.city = city;
		return wilder;
	}
	
	const wilderActions = {
		sayHello: function() {
			return  `hello I'm ${this.firstName}`;
		}
	};

 - the prototype (*wilderActions*) isn't in the function, we can reach it through the &lowbar;&lowbar;proto&lowbar;&lowbar; in the 2nd line. 



![Another example for __proto__ and prototype](https://i.imgur.com/ZxzPqFK.jpg)


We can make it shorter using the **"New"** keyword:

    function  CreateWilder(firstName, city) {
    // will create automaticaly a this object
    this.firstName = firstName,
    this.city = city;
    // will automatically return
    }
    
    CreateWilder.prototype.sayHello = function(){
    // we put this function to our main function prototype
	    return  `hello I'm ${this.firstName}`;
	};
	
	const wilder1 = new CreateWilder(“Mia”, “Berlin”);

 - the **capital starting letter** of the function name indicates to other developers that they can use the "new" keyword.
 - *wilder1* inherit from *CreateWilder* prototype => **prototypal inheritence**
 - if we console.log an array, inside the &lowbar;&lowbar;proto&lowbar;&lowbar; we can see push, pop, slice, sort, etc., all the methods that we can use  => every time we create an array, it inherits from the parent, that's why we can use these methods => it's the same with objects, functions

There is no Class, just fake one with prototype.

Example for classical prototypal inheritence: 

    let  Person = function (name, city) {
	    // when we use Call, this will refer to Student
	    this.name = name;
	    this.city = city;
	};
	
	Person.prototype.sayHello = function () {
		return  `Hello, I'm ${this.name}`;
	};
	
	let  Student = function (name, city, campus) {
		// We want to have also the name and the city from the
		// Person function, so we are calling it
		Person.call(this, name, city);
		this.campus = campus;
	};
	
	Object.setPrototypeOf(Student, Person.prototype);
	// We are "linking" Student to the Person prototype

And for modern fake-Class one:

    class  Person1 {
	    constructor(name, city) {
		    this.name = name;
		    this.city = city;
		}
		sayHello() {
			return  `Hello, I'm ${this.name}`;
		}
	}
	
	class  Student1  extends  Person1 {
		constructor(name, city, campus) {
			super(name, city);
			this.campus = campus;
		}
	}

 - both are valid





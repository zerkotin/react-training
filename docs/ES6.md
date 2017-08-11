# ES6 Prerequisites
It is possoble to write react apps with ES5, but ES6 has some great features you would like to use.

- classes `class foo {}`
- `let` and `const`
- arrow functions `=>`
- destruction `{foo, bar} = o;`
- `...` operator
- `Object.assign`

You can learn about it in detail with the book [You-Dont-Know-JS](http://github.com/getify/You-Dont-Know-JS)  
Under: ES6 & Beyond -> Chapter 2: Syntax  

Lets go through the highlights quickly...

## classes
ES6 class syntax with a constructor
```javascript
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
}

//polluting the global scope
user = new User('John', 'Smith');
user.name; //John
user.email; //Smith
```

## super
lets extend User class
```javascript
class Worker extends User {
  constructor(name, email, company) {
    super(name, email); //look at that
    this.company = company;
  }
}
```
you can't even imagine how much boilerplate code is saves, if you want to have an idea you can take a look at my [Javascript training](http://github.com/zerkotin/javascript) under: `prototypes.js`

## concise
concise function syntax
```javascript
//in classes
class Foo {
  addBar(bar) {//this is a function
    //do something with bar
  }
}

//or in objects
foo = {
  doSomething() { //this is a function
    //do something
  }
}
```

## const and let
`const` and `let` are somewhat like `var` but like the name suggests, `const` is a constant.  
both `const` and `let` differ from `var` by being __block scoped__ as opposed to the __function scoped__ `var`.

const example
```javascript
const x = 1;
x =  2; //error! you can't reassign a const!
```
let example
```javascript
let arr = [];
for(let i = 0; i< 10; i++){
  arr.push(function(){return i});
}
arr[2](); //2
arr[3](); //3
i; //reference error!
```
same code written with a `var` would have printed `10` as the output of `arr[2]();` or any other number for that matter.  
in addition `i;` would have printed `10` as well and would not produce an error.  

## arrow functions
arrow functions are not just shorter, they also share the same `this` as where they are being called from.  
ES5 syntax problem
```javascript
const foo = (prefix, suffix) => prefix + suffix; //create a function
foo('John', 'Smith'); //JohnSmith

const arr = [1, 2, 3, 4];
const mapped = arr.map(i => i + 1); //use as callback
mapped; //2, 3, 4, 5

function SomeClass(service) {
  this.response = null;
  service.somethingAsync(response => this.response = response); //short and to the point
}
```
The last example with `SomeClass` would need a `var that = this;` solution or `binding`, arrow functions make it easier.  

## destruction
concise and destruction are very useful
```javascript
let o = {name: 'John', last: 'Smith', email: 'john@smith.i'};
let {name, email} = o;
name; //John
email; //john@smith.i

//now lets use concise
let x = {name, email};
x; //{name: 'John', email: 'john@smith.i'}

//a useful example
const foo = ({name, last, email}) => { //destruction
  console.log(`name: ${name}, last name: ${last}, email: ${email}`); //ES6 template strings
};
foo(o); //name: John, last name: 'Smith', email: john@smith.i
```

## ... operator
the spread/rest operator can be used to group/ungroup.
```javascript
//array
const arr = [1,2,3,4];

//function with 4 parameters
function foo(a, b, c, d) {
  return a + b + c + d;
}

//spread
foo(...arr); //10

//rest
function bar(...arr) {
  return arr.length;
}

bar(1, 2, 3, 4, 5, 6); //6

//concatenating arrays
let concatenated = [...arr, 5, 6, 7, 8, 9, 10];
concatenated; //1, 2, 3, 4, 5, 6, 7, 8, 9, 10

```

## Object.assign
`Object.assign` is a very useful addition to Object its receives parameters in the form of `(target, source...)` and returns the `source`.  
in short, it merges object properties.
```javascript
let name = 'John';
let last = 'Smith';
let email = 'john@smith.i';
let phone = '555-123456';
let someone = {name, last, email}; //note the concise assignment

//using object assign
let someoneElse = Object.assign({}, someone, {phone});
someone; //{name: 'John', last: 'Smith', email: 'john@smith.i'}
someoneElse; //{name: 'John', last: 'Smith', email: 'john@smith.i', phone: '555-123456'}

//another way
someoneElse = {phone};
Object.assign(someoneElse, someone);
someone; //{name: 'John', last: 'Smith', email: 'john@smith.i'}
someoneElse; //{name: 'John', last: 'Smith', email: 'john@smith.i', phone: '555-123456'}
```
Just don't forget! the last target overrides previous properties with the same name!

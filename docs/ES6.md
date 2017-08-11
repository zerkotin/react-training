# ES6 Prerequisites
It is possoble to write react apps with ES5, but ES6 has some great features you would like to use.

- classes `class foo {}`
- `let` and `const`
- arrow functions `=>`
- destruction `{foo, bar} = o;`
- `...` operator
- `Object.assign`

You can learn about it in detail with the book [You-Dont-Know-JS](github.com/getify/You-Dont-Know-JS)  
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
you can't even imagine how much boilerplate code is saves, if you want to have an idea you can take a look at my [Javascript training](github.com/zerkotin/javascript) under: `prototypes.js`

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
both `const` and `let` differ from `var` by being __block scoped__ as opposed to the __function scoped__ `var`  
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

## destruction
arrow functions are not just shorter, they also share the same `this` as where they are being called from.  
ES5 syntax problem
```javascript
function Foo() {
  this.x = 1;
  this.run = function() {
    setTimeout(function(){
      console.log(this.x); //undefined
    }, 1000);
  }
}
```
arrow function solution
```javascript
class Foo {
  constructor() {
    this.x = 1;
  }
  run() {
    setTimeout( () => console.log(this.x), 1000); //1
  }
}
```

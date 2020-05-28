# Stateless Components
reacts simplest component is called a stateless component

## How to write a component
a component is a function that receives 'props'
```javascript
const Greeting = (props) => <div>{props.name}</div>; //using an arrow function

//or a function
function Greeting(props) { // the preferable way
  return <div>{props.name}</div>;
}
```
note the `{props.name}` - when writing DOM elements you can evaluate javascript expressions inside curly brackets.  
`props` is the way react components pass data down the chain.

## How to use
so we wrote a Component, but how do i use it?  
```javascript
import React from 'react';
import {render} from 'react-dom';

const Greeting = (props) => <div>{props.name}</div>;

render(<Greeting name="John" />, document.getElementById('app')); //there
```
we have a website that says John!

## Some default props and Events examples
there are some react reserved props
- className - instead of the usual html property `class`
- onClick - for click events
- onChange - for handling `<input>` change events
- some react addons like `react-router` add more props to components

- since we are writing Javascript and HTML on the same file, let's establish some basic rule of code styling. use single quotes `'text'` for javascript and double quotes `"text"` for HTML.

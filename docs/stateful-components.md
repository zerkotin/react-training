# Stateful Components
stateful components as the name implies have a state and are dynamic

## how to write
```javascript
import {React} from 'react'; //destruct React object from 'react' library

class Toggle extends React.Component { //now its a class, not a function
  constructor (props){ //constructor with props
    super(props); //have to call super...

    this.state = {toggle: true}; //applying initial state to the component

    this.toggle = this.toggle.bind(this); //bind for outside calls
  }

  //a utility function called onClick
  toggle() {
    this.setState( previousState => {toggle: !previousState.toggle}); //toggling the toggle state
  }

  //render method will be called when the state change
  render() {
    return(
      <div className="toggle" onClick={this.toggle}>
        {this.state.toggle? 'on' : 'off'}
      </div>
    );
  }
}
```

### a small breakdown
more about state a little later  
first let's break it down the render part

- `render()` - the render method will be called every time the state changes
- `return` - a render method must return an HTML element
- `className="toggle"` - the `className` prop replaces the `class` property of regular HTML elements
- `onClick={this.toggle}` - binding 'click event' to `toggle` function of the class
- `{this.state.toggle? 'on' : 'off'}` - javascript that returns 'on'/'off' according to state.toggle property

## the State
just like `props` the `state` is also a reserved name.  
rules regarding state
- change data in the state with `this.setState` function
- keep the data you store in the state immutable
### 2 ways to use `setState`
1. `setState` can receive a function with previous state as an argument
```javascript
toggle() {
  this.setState( previousState => !previousState.toggle ); //arrow function with previous state
}
```
state changes are async, whenever you are changing data progressively, you should use this method.

2. `setState` can receive an `Object`
```javascript
toggle() {
  this.setState({toggle: false}); //object
}
```
when using an `Object` as the argument in `setState` we can set a partial state, and only the keys we provide will change, the rest will remain untouched.


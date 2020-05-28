[The official React component lifecycle page](https://reactjs.org/docs/react-component.html "Component Lifecycle")

# Component lifecycle
The component lifecycle is made of 3 parts
1. Mount
2. Update
3. Unmount

## Mounting
Mounting occurs when a component is being assigned to the DOM and is set to be rendered.  
mounting fires the following functions in the component and in that specific order
1. `constructor(props)`
2. `static getDerivedStateFromProps(props, state)`
3. `render`
4. `componentDidMount` - _this is where we usually make our AJAX calls_

## Updating Props/State
The following functions are called when there's an update to either `props` or `state` and are in that order  
1. `static getDerivedStateFromProps(props, state)`
2. `shouldComponentUpdate(nextProps, nextState)` - _return false to prevent component from rendering on certain conditions_
3. `render`
4. `getSnapshotBeforeUpdate(prevProps, prevState)`
5. `componentDidUpdate(prevProps, prevState, snapshot)`

_**note** unless `shouldComponentUpdate` returns `false` react will render on every `prop` and `state` change._

## Unmounting
Unmounting occurs when a component is being removed from the DOM.  
this is where you want to remove any Event listeners you have initiated in this component.
1. `componentWillUnmount`

```javascript
//skipping the imports and class declarations
componentDidMount() {
  //updating state.name from URL #
  this.historyListener = this.props.history.listen(location => this.setState({name: location.hash.slice(1)});
}

componentWillUnmount {
  this.historyListener(); //removing history listerner
}
```
This is an example of using mount and unmount in order to register an event listener and removing the listener when unmounting  

## Note
There is also `forceUpdate` but it is not recommend to use it. as a general rule of thumb, if you need to use it you probably didn't think it through.

## Complete Example
```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {clicked: false}
    
    this.handleClick=this.handleClick.bind(this);
  }
  
  static getDerivedStateFromProps(props, state) {
    return {
      clicked: props.clicked
    };
  }
  
  shouldComponentUpdate(nextProps, nextState) {
    return this.props.clicked !== nextProps.clicked || this.state.clicked !== nextState.clicked;
  }
  
  render() {
    
    return <div className={this.state.clicked ? "clicked" : ""} onClick={this.handleClick}>Click Me</div>;
  }
  
  componentDidMount() {
    fetch('1.json').then(r => console.log(r));
  }
  
  getSnapshotBeforeUpdate(prevProps, prevState) {
    // scrollbar calculations?!
  }
  
  componentDidUpdate(prevProps, prevState, snapshot) {
    // post update calculations
  }
  
  componentWillUnmount() {
    // deregister from external events
  }
  
  
  handleClick() {
    this.setState({clicked: true});
  }
}
```

You can play around with the example [Here](https://codepen.io/zerkotin/pen/QWjXgYB "Codepen.io")


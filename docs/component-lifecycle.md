[The official React component lifecycle page](https://reactjs.org/docs/react-component.html "Component Lifecycle")

# Component lifecycle
The component lifecycle is made of 3 parts
1. Mount
2. Update
3. Unmount

## Mounting
mounting occurs when a component is being assigned to the DOM and is set to be rendered.  
mounting fires the following functions in the component and in that specific order
1. `constructor()`
2. `static getDerivedStateFromProps()`
3. `render`
4. `componentDidMount` - _this is where we usually make our AJAX calls_

## Updating Props/State
The following functions are called when there's an update to either `props` or `state` and are in that order  
1. `static getDerivedStateFromProps()`
2. `shouldComponentUpdate()` - _return false to prevent component from rendering on certain conditions_
3. `render`
4. `componentDidUpdate()`

_**note** unless `shouldComponentUpdate` returns `false` react will render on every `prop` and `state` change._

## Unmounting
unmounting occurs when a component is being removed from the DOM.  
this is where you want to remove any Event listeners you have initiated in this component.
1. `componentWillUnmount`

## Note
there is also `tnis.forceUpdate` but it is not recommend to use it. as a general rule of thumb, if you need to use it you probably didn't think it through.

## Example
consider the following code
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
this is an example of using mount and unmount in order to register an event listener and removing the listener when unmounting.

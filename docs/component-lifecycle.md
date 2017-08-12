# component lifecycle
component lifecycle is made of a few parts
1. mounting
2. updating props/state
3. unmounting

## mounting
mounting occurs when a component is being assigned to the DOM and is set to be rendered.  
mounting fires the following functions in the component and in that specific order
1. `constructor(props)`
2. `componentWillMount`
3. `render`
4. `componentDidMount` - _this is where we usually make our AJAX calls_

## updating props/state
the following functions are called when there's an update to either `props` or `state`
1. `componentWillReceiveProps(nextProps)` - _occurs before props change_
2. `shouldComponentUpdate(nextProps, nextState)` - _return false to prevent component from rendering on certain conditions_
3. `componentWillUpdate(nextProps, nextState)`
4. `render`
5. `componentDidUpdate(prevProps, prevState)`

## unmounting
unmounting occurs when a component is being removed from the DOM.  
this is where you want to remove any Event listeners you have initiated in this component.
1. `componentWillUnmount`

## note
there is also `tnis.forceUpdate` but i recommend not using it. as a general rule, if you need to use it you probably didn't think it through.

## example
consider the following code
```javascript
componentDidMount() {
  //updating state.name from URL #
  this.historyListener = this.props.history.listen(location => this.setState({name: location.hash.slice(1)});
}

componentWillUnmount {
  this.historyListener(); //removing history listerner
}
```
this is a real code, on some occasions you really need to unregister yourself from events.

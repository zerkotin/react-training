# controlled components
controlled components are react's way of 2 way binding  
example
```javascript
//skipping the imports and class declarations
constructor(props) {
  super(props);
  
  this.state = {value: 'default'};
}

render() {
  return <input onChange={e => this.setState({value: e.target.value})} value={this.state.value} />
}
```
the example above will initilize an `input` tag with `default` written in it and on every key stroke will update the `state`.  
note that `value` may not be `null`/`undefined`.

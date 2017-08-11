# JSX
JSX is allowing us to combine DOM elements in Javascript.  

## an element
```javascript
let helloElement = <div>hello</div>;
```

## a stateless component
```javascript
function Foo() {
  return <div>hello</div>;
}
```

## a statefull components
```javascript
class Foo extends React.Component {
  render() {
    return <div>hello</div>;
  }
}
```
That was simple wasn't it? we will dig into those components later on

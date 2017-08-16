# uncontrolled components
uncontrolled components are a good alternative when
- your values may include nulls
- you dont want to rerender/dispatch event on every keypress
- this is mostly useful in forms

example
```javascript
class FormView extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleSubmit() {
    console.log(this.nameInput.value);
  }

  render() {
    return (
      <div className="form-view">
        <div>Name: <input type="text" ref={(input) => this.nameInput = input}/></div>
        <div onClick={this.handleSubmit}>Submit</div>
      </div>
    );
  }
}
```

# router
the router allows us to use the browser's history to navigate through our application

simple example
```javascript
import React from 'react'; //needed on every file using JSX
import {render} from 'react-dom'; //needed for first render
import {HashRouter, Route, Switch, Link} from 'react-router-dom'; //Router imports

render(
  <HashRouter> {/*HashRouter/BrowserRouter - the entry point of Routing*/}
    <Switch> {/*use Switch when you want only one Route at a time to be rendered*/}
      <Route path="/" component={AppView}/> {/*a Route to render AppView - the entire application*/}
    </Switch>
  </HashRouter>
  ,document.getElementById('app') {/* the DOM element to render to*/]
);

//The application
function AppView(){
  return (
    <div className="app-view">
      {/*navigation*/}
      <Link to="/about">click to render about view</Link> {/*Link to /about*/}
      <Link to="/contact">click to render contact view</Link> {/*Link to /contact*/}
      {/*routes*/}
      <Switch>
        {/*Route will be rendered when clicking on about link*/}
        <Route path="/about" component={AboutView}/>
        {/*Route will be rendered when clicking on contact link*/}
        <Route path="/contact" component={ContactView}/> 
      </Switch>
    </div>
  );
}

//about view
function AboutView() {return <div>About</div>}
//contact view
function ContactView() {return <div>Contact</div>}
```
The example is a little big, but its the simplest application with a Router i could think of.  
if you go through it and read the comments its quite self explanatory.  
but nevertheless let's explain the different Tags.

## HashRouter
`HashRouter` is the main application entry or the parent of the routable components, you need to put it as the top of the hierarchy of the routable components.  
you may also use `BrowserRouter` but the HashRouter is less of a hussle in my oppinion.

## Switch
you don't have to use `Switch` but you can, `Switch` will only render 1 Route from the list of Routes it contains.  
without `Switch` you are able to match more than 1 Route to a path, and more than 1 can be rendered.

## Route (exact/path/component/render)
`Route` specifies a component to be rendered when a certain path matches.  
`Route` receives a `path` and a `component`/`render` as required props.  
`render` example
```javascript
<Route path="/somepage" render={(props) => <div>some page</div>}/>
//or
<Route path="/help" render={() => <HelpView category={this.state.selectedCategory}/>}/>
```
this is mostly helpful when wanting to pass on different props to the route.

another useful prop is `exact` which is used in a semantic way.  
example
```javascript
<Route exact path="/" component={LandingPage}/>
```
this is mostly used when dealing with a screen hierarchy of the form  
- `/users` - show a list of users 
- `/users/35` - show a user with id `35`
without `exact` they both match `/users` as a `path` prop

## Link
a `Link` is a clickable components that once clicked will change the URL to the one given through `to` prop.  
this will cause the router to render a component with a matching path.

## withRouter - programatically browsing
using `Link` we can browse the application, but sometimes we need Event driven browsing. for this we have `withRouter`.
the usage of `withRouter` will add to a component the following props
- `history`  - [docs on github](http://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/api/history.md)
- `location` - [docs on github](http://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/api/location.md)
- `match` - [docs on github](http://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/api/match.md)

the following example will create a component that shows the current URL path and follows it for changes
```javascript
//PathView.jsx
import React from 'react'
import { withRouter } from 'react-router'

class PathView extends React.Component {
  constructor(props) {
    super(props);
    //init state
    this.state = {path: null};
  }
  
  componentDidMount() {
     //listen to location change
     //set the state on location change
     //save the unlisten function for later use
    this.unlisten = this.props.history.listen(location => this.setState({path: location.path}));
  }
  
  componentWillUnmount() {
    //when unmounting - stop listening to route changes
    this.unlisten();
  }
  
  render() {
    return (
      <div>Path: {this.props.location.pathname}</div> {/*show the current location*/}
    )
  }
}
export default withRouter(PathView); //wrap the exported class withRouter
```

all the magic is done in the `export default withRouter(PathView)`, we are wrapping our component with extra functionality.
later on we can use the `PathView` without any change
```javascript
//HeaderView.jsx
import PathView from './PathView.jsx';
//skipping code
render() {
  return (
    <div className="header-view">
      {/*some elements for header view*/}
      <PathView /> {/*render the PathView withRouter*/}
     </div>
  );
}
```

but still how do i change route programatically?!
```javascript
//skipping imports
class LogoutView extends React.Component {
  render() {
    return <div onClick={() => this.props.history.push('/login')}>Logout</div>
  }
}
export default withRouter(LogoutView);
```
`this.props.history.push` - can be used at any point in the class to navigate to another screen.

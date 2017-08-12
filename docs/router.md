# router
the router allows us to use the browser's history to navigate through our application

simple example
```javascript
import React from 'react';
import {render} from 'react-dom';
import {HashRouter, Route, Switch, Link} from 'react-router-dom';

render(
  <HashRouter>
    <Switch>
      <Route path="/" component={AppView}/>
    </Switch>
  </HashRouter>
  ,document.getElementById('app')
);

function AppView(){
  return (
    <div className="app-view">
      <Link to="/about">click to render about view</Link>
      <Link to="/contact">click to render contact view</Link>
      <Switch>
        <Route path="/about" component={AboutView}/>
        <Route path="/contact" component={ContactView}/>
      </Switch>
    </div>
  );
}
function AboutView() {return <div>About</div>}
function ContactView() {return <div>Contact</div>}
```
To be continued..
1. HashRouter/BrowserRouter
2. Switch
3. Route (exact/path/component/render)
3. Link (to)
4. withRouter (history, location)

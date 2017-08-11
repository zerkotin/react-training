# Rendering
react's main feature is deciding when and which element to render, but how do we render the first page?  
we need an HTML page with a `<div id="app"></div>`  
it's bet practice to not render to the `body` of our HTML.

render example
```javascript
import React from 'react';
import {render} from 'react-dom'; //destructing the 'render' method from 'react-dom'

render(<div>hello</div>, document.getElementById('app')); //render to an element with id="app"
```
When rendering a different component on the same DOM element, react will 'unmount' the old one and 'mount' the new one instead.
_note that react does not 'like' when you use it more than once in your application, but for now you can..._

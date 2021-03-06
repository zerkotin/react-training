# prop-types
using prop-types you can define API to your components and provide type safety.  
_**note** prop-types should be installed using `npm i prop-types --save`_

example
```javascript
import React from 'react';
import PropTypes from 'prop-types'; //import prop-types

//a stateless component for FontAwesome
function Icon({name}) { //using destruction
  return <i className={'fa fa-' + name} aria-hidden="true"></i>;
}
//marking name as Required
Icon.propTypes = {
  name: PropTypes.string.isRequired
};
```

## More about prop-types
i will not specify all type options here, but we can take a look at the prop-types repo for examples.  
[prop-types on github](http://github.com/facebook/prop-types)

# Typescript
Another popular way to enforce typing is [Typescript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html "Typescript in 5 min")

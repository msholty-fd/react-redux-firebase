# isLoaded

Detect whether items are loaded yet or not

**Parameters**

-   `item` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Item to check loaded status of. A comma seperated list is also acceptable.

**Examples**

```javascript
import React, { Component, PropTypes } from 'react'
import { connect } from 'react-redux'
import { firebaseConnect, isLoaded, dataToJS } from 'react-redux-firebase'
```

Returns **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Whether or not item is loaded

# isEmpty

Detect whether items are empty or not

**Parameters**

-   `item` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Item to check loaded status of. A comma seperated list is also acceptable.
-   `data`  

**Examples**

```javascript
import React, { Component, PropTypes } from 'react'
import { connect } from 'react-redux'
import { firebaseConnect, isEmpty, dataToJS } from 'react-redux-firebase'
```

Returns **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** Whether or not item is empty

# toJS

Convert Immutable Map to a Javascript object

**Parameters**

-   `data` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Immutable Map to be converted to JS object (state.firebase)

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** data - Javascript version of Immutable Map

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Data located at path within Immutable Map

# pathToJS

Convert parameter from Immutable Map to a Javascript object

**Parameters**

-   `firebase` **[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)** Immutable Map to be converted to JS object (state.firebase)
-   `data`  
-   `path` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Path from state.firebase to convert to JS object
-   `notSetValue` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean))** Value to use if data is not available

**Examples**

_Basic_

```javascript
import { connect } from 'react-redux'
import { firebaseConnect, pathToJS } from 'react-redux-firebase'
```

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Data located at path within Immutable Map

# dataToJS

Convert parameter under "data" path of Immutable Map to a Javascript object.
**NOTE:** Setting a default value will cause `isLoaded` to always return true

**Parameters**

-   `firebase` **[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)** Immutable Map to be converted to JS object (state.firebase)
-   `data`  
-   `path` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Path of parameter to load
-   `notSetValue` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean))** Value to return if value is not
    found in redux. This will cause `isLoaded` to always return true (since
    value is set from the start).

**Examples**

_Basic_

```javascript
import { connect } from 'react-redux'
import { firebaseConnect, dataToJS } from 'react-redux-firebase'
```

_Default Value_

```javascript
import { connect } from 'react-redux'
import { firebaseConnect, dataToJS } from 'react-redux-firebase'
const defaultValue = {
 1: {
   text: 'Example Todo'
 }
}
```

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Data located at path within Immutable Map

# orderedToJS

Convert parameter under "ordered" path of Immutable Map to a
Javascript array. This preserves order set by query.

**Parameters**

-   `firebase` **[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)** Immutable Map to be converted to JS object (state.firebase)
-   `data`  
-   `path` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Path of parameter to load
-   `notSetValue` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean))** Value to return if value is not found

**Examples**

_Basic_

```javascript
import { connect } from 'react-redux'
import { firebaseConnect, orderedToJS } from 'react-redux-firebase'
```

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Data located at path within Immutable Map

# populatedDataToJS

Convert parameter under "data" path of Immutable Map to a
Javascript object with parameters populated based on populates array

**Parameters**

-   `firebase` **[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)** Immutable Map to be converted to JS object (state.firebase)
-   `data`  
-   `path` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Path of parameter to load
-   `populates` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)** Array of populate objects
-   `notSetValue` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean))** Value to return if value is not found

**Examples**

_Basic_

```javascript
import { connect } from 'react-redux'
import { firebaseConnect, helpers } from 'react-redux-firebase'
const { dataToJS } = helpers
const populates = [{ child: 'owner', root: 'users' }]

const fbWrapped = firebaseConnect([
  { path: '/todos', populates } // load "todos" and matching "users" to redux
])(App)

export default connect(({ firebase }) => ({
  // this.props.todos loaded from state.firebase.data.todos
  // each todo has child 'owner' populated from matching uid in 'users' root
  // for loading un-populated todos use dataToJS(firebase, 'todos')
  todos: populatedDataToJS(firebase, 'todos', populates),
}))(fbWrapped)
```

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Data located at path within Immutable Map

# customToJS

Load custom object from within store

**Parameters**

-   `firebase` **[Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)** Immutable Map to be converted to JS object (state.firebase)
-   `path` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Path of parameter to load
-   `customPath` **[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Part of store from which to load
-   `data`  
-   `custom`  
-   `notSetValue` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean))** Value to return if value is not found

**Examples**

_Basic_

```javascript
import { connect } from 'react-redux'
import { firebaseConnect, helpers } from 'react-redux-firebase'
const { customToJS } = helpers

const fbWrapped = firebaseConnect(['/todos'])(App)

export default connect(({ firebase }) => ({
  // this.props.todos loaded from state.firebase.data.todos
  requesting: customToJS(firebase, 'todos', 'requesting')
}))(fbWrapped)
```

Returns **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** Data located at path within state

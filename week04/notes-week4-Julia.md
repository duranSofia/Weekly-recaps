## React.js Introduction

* Developed by Facebook, first version 2013
* open source library, not framework
* to solve the problem of complex states changing without reloading the rest of the DOM
* compares state of what you are writing with Virtual DOM and changes what needs to be changed in the view port
that's what makesit so fast
* Can use it on the DOM, mobile apps (React.native) and terminal
* Used by Netflix, Airbnb, Instagram …

### Components

* Core concept
* React splits the UI into components
* component hierarchy: component can contain multiple components (children)
* Conceptually, components are like JavaScript functions
* accept arbitrary inputs (called "props") and return React elements describing what should appear on the screen

#### Types of components

• Class components vs Functional components (and container)

##### Class component

• class inherits from React.Component
• the render() method must return JSX or null
• Class components MUST have a render method
• and always needs to return() something
• component that needs to be aware of its own state: a javascript object used to record and react to user events
• when a component state is changed, the component rerenders (plus its child components) - to use state inside a component, you need to initialize the state object


Example:

```
import React, { Component } from 'react'; //destructured ```
class Welcome extends Component { //destructured
  constructor(props) {
    super(props);
    this.state = { message: 'Welcome to the Welcome Page!'};
  }
  
  render() {
    return (
      <div className="welcome-component">
        {this.state.message}
      </div>
    );
  }
}

export default Welcome;
````

#### Functional Component

• regular JS function
• Less code in functional components
• name must start with a capital letter
• must return JSX or null

```
import React from 'react';

const ExampleComponent = ({message}) => {
  const showMessage = (event) => {
     alert(`The message is: ${message}`);
   };
   
   return (
    <div>
      <a href="#" onClick={showMessage}>show me</a>
    </div>
   );
  }
 
 export default ExampleComponent;
 ````
 
 
### JSX


• JSX = Javascript + XML
• neither HTML nor a string
• JSX is a statically-typed, object-oriented programming language designed to run on modern web browsers
• faster: performs optimization while compiling the source code to JavaScript
• safer: statically-typed and mostly type-safe, many errors caught during compilation process
• easier: offers a solid class system, without having to use prototype-based inheritance system provided by JavaScript



#### Nested Elements
• to return more elements, we need to wrap it with one container element


App.jsx

```
import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <h1>Header</h1>
            <h2>Content</h2>
            <p>This is the content!!!</p>
         </div>
      );
   }
}
export default App;
```

### JavaScript Expressions
• JavaScript expressions must be wrapped it with curly brackets {}

The example renders “2”.

```

import React from 'react';

class App extends React.Component {
   render() {
      return (
         <div>
            <h1>{1+1}</h1>
         </div>
      );
   }
}
export default App;
````

#### Conditions

• cannot use if else statements inside JSX!
• instead conditional (ternary) expressions

```
import React from 'react';

class App extends React.Component {
   render() {
      var i = 1;
      return (
         <div>
            <h1>{i == 1 ? 'True!' : 'False'}</h1>
         </div>
      );
   }
}
export default App;
```

#### Styling

• React recommends using inline styles
• camelCase syntax.

```
import React from 'react';

class App extends React.Component {
   render() {
      var myStyle = {
         fontSize: 100,
         color: '#FF0000'
      }
      return (
         <div>
            <h1 style = {myStyle}>Header</h1>
         </div>
      );
   }
}
export default App;
```

### Naming Convention

• HTML tags use lowercase tag names
• React components start with Uppercase
• use className and **htmlFor **as XML attribute names instead of class and for



### Tooling
React apps require third party tools to run

### Webpack
• is a bundler
• mashes all .js files and .css files into one .js and one .css

### Babel
• Javascript transpiler
• makes newest JS features compatible with most browsers

### Setup
• Create React App: configures all the necessary tools
• npx create-react-app (package runner tool that comes with npm 5.2+)
• downside is less flexibility and more files than needed

React Props
• a React application has components
• are hierarchically organized
• based on a main component (App by default)
• Props enable a parent component to pass information to a child component
• only in this way
• Props are arguments passed into React components
• are passed to components via HTML attributes
• Example Add a "brand" attribute to the Car element:


```
const myelement = <Car brand="Ford" />;
```

The component receives the argument as a props object:

```

class Car extends React.Component {
  render() {
    return <h2>I am a {this.props.brand}!</h1>;
  }
}
```



Props pass Data from one component to another, as parameters. Send the "brand" property from the Garage component to the Car component:
```
class Car extends React.Component {
  render() {
    return <h2>I am a {this.props.brand}!</h2>;
  }
}

class Garage extends React.Component {
  render() {
    return (
      <div>
      <h1>Who lives in my garage?</h1>
      <Car brand="Ford" />
      </div>
    );
  }
}

ReactDOM.render(<Garage />, document.getElementById('root'));

```

### Access props
• are accessible in the child component (read only):
• via this.props in a class component
• via props in a functional component

### Prop types
•  Contrary to the attributes passed to markup, props can be of any datatype: Boolean, number, string, object, array, function, etc.

### Boolean props
• special case!
• not necessary to pass a true/false value, just the prop name

```
render() {
    // No need for "released={true}"!
    return (
        <Movie
            released
        />
    )
}
render() {
    // This will work the same way as if you passed "released={false}"!
    return (
        <Movie />
    )
}

```
If the boolean value is contained within a variable, the you'll have to pass it.
```
render() {
    let booleanVariable = true; // this will often be calculated
    return (
        <Movie
            released={booleanVariable}
        />
    )
}
```

### Destructuring props
•  good practice: to improve readability


```
render() {
    return (
      <section>
        {this.props.loading ? (
          <div className="loader">
            <ClipLoader color={'white'} loading={this.props.loading} />
          </div>
        ) : (
          <div className="results">
            {this.props.error.errorHappened ? (
              <h1>{this.props.error.errorMsg}</h1>
            ) : (
                <div>No Error </div>
          </div>)
    </section>
   ```
   
 
** Destructuring the props:
```
render() {
const { loading, errorMsg, errorHappened } = this.props
    return (
      <section>
        {loading ? (
          <div className="loader">
            <ClipLoader color={'white'} loading={loading} />
          </div>
        ) : (
          <div className="results">
            {errorHappened ? (
              <h1>{errorMsg}</h1>
            ) : (
                <div>No Error </div>
          </div>)
    </section>
    
```
    
    
### Using the spread operator
•  to pass all key/values of an object as individual props
• it can also:
• Copying an array
• Concatenating or combining arrays
• Using Math functions
•  Using an array as arguments
• Adding an item to a list
• Adding to state in React
• Combining objects
• Converting NodeList to an array

Example: without



function App() {
  return <Hello firstName="Ahmed" lastName="Bouchefra" />;
}
Using the Spread operator, you would write the following code instead:

function App() {
  const props = {firstName: 'Ahmed', lastName: 'Bouchefra'};
  return <Hello {...props} />;
}
```

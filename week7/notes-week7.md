
## React Hooks
Hooks are a new React "invention"- they introduced them in October 2018. With them we can use functional components in React instead of the good old class components.

Why are they good?

Cleaner code, less repetition.

No more:

```
constructor(props) {
this.updateRepos = this.updateRepos.bind(this)
}
```

### UseState

we can use states with functions, yaay!
```
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

this would be longer to code with class components:

```
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}

```


The complicated lifecycle methods (ComponentDidMount, WillUpdate,WillUnmount) can be also done with hooks. The most used hooks:

### UseEffect

is a React hook where you can apply side effects, for example, getting data from server. Here is the place we fetch the API. Two arguments:

The first is a callback function to run.

The second argument is an array of values (usually props) to react to.

If any of the value in the array changes, the callback will be fired after every render. When it's not present, the callback will always be fired after every render.

Comparison of lifecycle methods with useEffect:

```
componentDidMount() {
  console.log('mounted or updated');
}

componentDidUpdate() {
  console.log('mounted or updated');
}

useEffect(() => console.log('mounted or updated'));
componentWillUnmount() {
  console.log('will unmount');
}

useEffect(() => {
  return () => {
    console.log('will unmount');
  }
}, []);
```


### UseContext

it is a useful feature my big applications, if we want to make data (e.g. databases, API fetch, themes) globally available. Instead of passing local data around and through several layers of components, it takes a step back to create global state, which is extremely useful for data that needs to be shared across components (data such as themes, authentication, preferred language, etc.)


```
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);

  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );
}
```


### UseReducer

it is a "magic button", it lets you change the state. It accepts a reducer function with the application initial state, returns the current application state, then dispatches a function.

Here is an example of how it is used- to create counter buttons and also change the state in the meantime with less code:

```
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```


###  Error Boundaries

A JavaScript error in a part of the UI shouldn’t break the whole app. To solve this problem for React users, React 16 introduces a new concept of an “error boundary”.

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them. A class component becomes an error boundary if it defines either (or both) of the lifecycle methods static getDerivedStateFromError() or componentDidCatch(). Use static getDerivedStateFromError() to render a fallback UI after an error has been thrown. Use componentDidCatch() to log error information.


```
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
 
Then you can use it as a regular component:

<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>


```

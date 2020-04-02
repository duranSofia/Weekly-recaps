# Redux

- open-source JavaScript library for managing application state. 
It is most commonly used with libraries/frameworks such as React or Angular for building user interfaces. 


set up : 
### NPM
npm install redux

### Yarn
yarn add redux

OR 



### There are 3 main principles of Redux :

1.  Single source of truth: the data is centralised in a single state object, stored in the **store**

2.  State is read-only: the state is immutable, you never change it directly. (**State immutability** )

React requires data to be stored in a state via the setState() method which is not directly mutable.
With Redux, you do not modify the state stored in the store, you recalculate it completely.


3.  Changes are made with pure functions: the new state value is calculated via a function (**reducer**)

- A reducer is a pure function that allows you to calculate the new state value from two data inputs:
 * The current value of the state
 * An action that describes the type of change to be made
A pure function is predictable (no use of random function, network calls, etc.)


#### STORE 
The Redux createStore method is called by passing the reducer (here rootReducer) as a parameter to initialise the store.

```
import { createStore } from "redux";
import rootReducer from "../reducers/index";

const store = createStore(rootReducer);

export default store;

```

#### REDUCER 
- The initial value of the state can be described by storing it in the constant  initialState, which will be used by the reducer to initialise the state (in this example, the application is started with some pre-filled tasks).
 ( When the reducer is called for the first time, the state takes the value of  initialState.)

```
import {NAME_OF-THE-ACTION} from "../constants/index";

const initialState = {
  tasks: [
  { 
  id: 0, 
  title: "take out trash", 
  done: false 
  },
    { 
  id: 1, 
  title: "watch a movie", 
  done: false 
  },
    { 
  id: 2, 
  title: "call dad", 
  done: true 
  }
  ]
};

const rootReducer (state=initialState, action)=>{
switch (action.type) {
    case NAME_OF-THE-ACTION:
      return {
        ...state,
        tasks: [
          ...state.tasks,
          { id: state.tasks.length, title: action.title, done: false }
        ]
      };
        default:
      return state;
}
export default rootReducer;
```

#### ACTIONS 




#### CHANGING THE STATE 

To make a change, we send (**dispatch**) an action to the store: store.dispatch(...)

Here the select allows you to choose the filter. When it changes, the action of type CHANGE_FILTER is dispatched, with a filter attribute taking the value of the chosen option.
```
const filterSelector = document.querySelector(
 'select#filter-selector'
);
filterSelector.addEventListener(
 'change', event => store.dispatch({
   type: 'CHANGE_FILTER',
   filter: event.target.value
 })
);


```




with React 


redux template :
```
npx create-react-app my-app --template redux
```

# Redux Counter Example

This is a simple example of a counter application using Redux with React.

## Installation

First, make sure you have Node.js installed. Then, install the required dependencies.

```bash
npm install redux react-redux
```

## Project Structure

```css
src/
├── actions/
│   └── index.js
├── reducers/
│   └── counter.js
├── store/
│   └── index.js
├── components/
│   └── Counter.js
├── App.js
└── index.js
```

## Actions

Define the action types and action creators for incrementing and decrementing the counter.

```js
// src/actions/index.js
export const INCREMENT = "INCREMENT";
export const DECREMENT = "DECREMENT";

export const increment = () => ({
    type: INCREMENT,
});

export const decrement = () => ({
    type: DECREMENT,
});
```

## Reducer

Define the reducer that will handle the actions and update the state accordingly.

```js
// src/reducers/counter.js
import { INCREMENT, DECREMENT } from "../actions";

const initialState = {
    count: 0,
};

const counterReducer = (state = initialState, action) => {
    switch (action.type) {
        case INCREMENT:
            return { ...state, count: state.count + 1 };
        case DECREMENT:
            return { ...state, count: state.count - 1 };
        default:
            return state;
    }
};

export default counterReducer;
```

## store

Set up the Redux store by combining reducers and applying any middleware if needed.

```js
// src/store/index.js
import { createStore } from "redux";
import counterReducer from "../reducers/counter";

const store = createStore(counterReducer);

export default store;
```

## React Component

Create a React component that connects to the Redux store and dispatches actions.

```js
// src/components/Counter.js
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "../actions";

const Counter = () => {
    const count = useSelector((state) => state.count);
    const dispatch = useDispatch();

    return (
        <div>
            <h1>Counter: {count}</h1>
            <button onClick={() => dispatch(increment())}>Increment</button>
            <button onClick={() => dispatch(decrement())}>Decrement</button>
        </div>
    );
};

export default Counter;
```

## Connect Redux to React

Use the Provider component from React-Redux to connect the Redux store to the React application.

```js
// src/App.js
import React from "react";
import { Provider } from "react-redux";
import store from "./store";
import Counter from "./components/Counter";

const App = () => (
    <Provider store={store}>
        <Counter />
    </Provider>
);

export default App;
```

## Render the App

Ensure your app is rendered to the DOM.

```js
// src/index.js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
```

ReactDOM.render(<App />, document.getElementById('root'));

## Running the Application

To start the application, run:

```bash
npm start
```

Open your browser and navigate to http://localhost:3000 to see the counter application in action.

## Summary

This simple example demonstrates the basic structure of a Redux application integrated with React. It includes actions, reducers, the Redux store, and a connected React component.

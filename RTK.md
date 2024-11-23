# Redux Toolkit Counter Example

This is a simple example of a counter application using Redux Toolkit with React.

## Installation

First, make sure you have Node.js installed. Then, install the required dependencies.

```bash
npm install @reduxjs/toolkit react-redux
```

## Project Structure

```css
src/
├── features/
│   └── counterSlice.js
├── store/
│   └── index.js
├── components/
│   └── Counter.js
├── App.js
└── index.js
```

## Counter Slice

Define the slice that contains the reducer logic and action creators.

```js
// src/features/counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
    name: 'counter',
    initialState: {
        count: 0,
    },
    reducers: {
        increment: (state) => {
            state.count += 1;
        },
        decrement: (state) => {
            state.count -= 1;
        },
    },
});

export const { increment, decrement } = counterSlice.actions;

export default counterSlice.reducer;

```

## Store

Set up the Redux store using configureStore from Redux Toolkit.

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
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from '../features/counterSlice';

const Counter = () => {
    const count = useSelector((state) => state.counter.count);
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
import React from 'react';
import { Provider } from 'react-redux';
import store from './store';
import Counter from './components/Counter';

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
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));

```

## Running the Application

To start the application, run:

```bash
npm start
```

Open your browser and navigate to http://localhost:3000 to see the counter application in action.

## Summary

This simple example demonstrates the basic structure of a Redux application integrated with React using Redux Toolkit. It includes a slice, the Redux store, and a connected React component.

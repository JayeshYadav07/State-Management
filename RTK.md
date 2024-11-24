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
├── page/
│   └── todoSlice.tsx
│   └── todo.tsx
├── app/
│   └── store.tsx
├── App.tsx
└── index.tsx
```

## Counter Slice

Define the slice that contains the reducer logic and action creators.

```tsx
// src/page/todoSlice.js
import { createSlice } from "@reduxjs/toolkit";

const todoSlice = createSlice({
	name: "anything",
	initialState: {
		todos: [],
	},
	reducers: {
		addTodo: (state: any, action) => {
			// action.payload = object
			state.todos.push(action.payload);
		},
		removeTodo: (state, action) => {
			// action.payload = string
			state.todos = state.todos.filter(
				(todo: any) => todo.id !== action.payload
			);
		},
	},
});

export const { addTodo, removeTodo } = todoSlice.actions;
export default todoSlice.reducer;

```

## Store

Set up the Redux store using configureStore from Redux Toolkit.

```tsx
// src/app/store.js
import { configureStore } from "@reduxjs/toolkit";
import todoReducer from "../page/todoSlice";

const store = configureStore({
	reducer: {
		todo: todoReducer,
	},
});

export default store;
```

## React Component

Create a React component that connects to the Redux store and dispatches actions.

```tsx
// src/page/todo.tsx
import { useDispatch, useSelector } from "react-redux";
import { addTodo, removeTodo } from "./todoSlice";
import { useState } from "react";
function Todo() {
	const dispatch = useDispatch();
	const [title, setTitle] = useState("");
	const todos = useSelector((state: any) => state.todo.todos);
	return (
		<div>
			<div>
				<h1>Todos</h1>
				<input
					type="text"
					name="title"
					value={title}
					onChange={(e) => setTitle(e.target.value)}
				/>
				<button
					onClick={() =>
						dispatch(addTodo({ id: Date.now(), title: title }))
					}
				>
					Add
				</button>
			</div>
			<table>
				<thead>
					<tr>
						<th>Title</th>
						<th>Delete</th>
					</tr>
				</thead>
				<tbody>
					{todos.map((todo: any) => (
						<tr key={todo.id}>
							<td>{todo.title}</td>
							<td onClick={() => dispatch(removeTodo(todo.id))}>
								remove
							</td>
						</tr>
					))}
				</tbody>
			</table>
		</div>
	);
}

export default Todo;

```

## App component

```tsx
// src/App.js
import Todo from "./page/todo";

function App() {
	return (
		<div>
			<Todo />
		</div>
	);
}

export default App;
```

## Render the App

Use the Provider component from React-Redux to connect the Redux store to the React application.

```tsx
// src/index.js
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.tsx";
import { Provider } from "react-redux";
import store from "./app/store.tsx";

createRoot(document.getElementById("root")!).render(
	<StrictMode>
		<Provider store={store}>
			<App />
		</Provider>
	</StrictMode>
);


```

## Running the Application

To start the application, run:

```bash
npm run dev
```

Open your browser and navigate to http://localhost:5173 to see the counter application in action.

## Summary

This simple example demonstrates the basic structure of a Redux application integrated with React using Redux Toolkit. It includes a slice, the Redux store, and a connected React component.

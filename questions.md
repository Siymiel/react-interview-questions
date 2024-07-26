# React Interview Questions
*Author: Samuel Kinuthia*


### 1. What is React?

**Answer:**
React is a JavaScript library for building user interfaces, particularly single-page applications where you need a fast and interactive user experience. It allows developers to create large web applications that can change data without reloading the page. React is maintained by Facebook and a community of individual developers and companies.

### 2. What are the main features of React?

**Answer:**
The main features of React include:
- **JSX**: A syntax extension for JavaScript that allows you to write HTML directly within React.
- **Components**: Reusable and isolated pieces of code that return React elements to be rendered to the page.
- **Virtual DOM**: React creates a virtual representation of the real DOM, which allows it to perform optimizations by updating the real DOM only where necessary.
- **One-way Data Binding**: Data flows in one direction, making it easier to debug and understand.
- **State and Props**: `State` is mutable and managed within the component, while `Props` are immutable and passed down from parent to child components.

### 3. Explain the concept of “state” in React.

**Answer:**
State in React is an object that determines how a component renders and behaves. State is managed within the component and can change over time, usually as a result of user actions or network responses. When the state changes, the component re-renders to reflect the new state.

### 4. What is the difference between state and props?

**Answer:**
- **State**: State is managed within the component and is mutable. It holds information about the component's current situation and can be changed using `setState`.
- **Props**: Props are read-only, immutable, and passed from a parent component to a child component. Props allow data to flow between components and enable component reusability.

### 5. What is JSX?

**Answer:**
JSX stands for JavaScript XML. It is a syntax extension for JavaScript that looks similar to HTML and is used in React to describe what the UI should look like. JSX allows you to write HTML structures within JavaScript code, which gets transformed into React elements.

### 6. How do you create a React component?

**Answer:**
There are two main ways to create a React component:
1. **Function Components**:
   ```javascript
   function MyComponent() {
     return <div>Hello, World!</div>;
   }
   ```

2. **Class Components**:
   ```javascript
   class MyComponent extends React.Component {
     render() {
       return <div>Hello, World!</div>;
     }
   }
   ```

### 7. What is the virtual DOM?

**Answer:**
The virtual DOM is a lightweight copy of the actual DOM. It is kept in memory and synced with the real DOM by a library such as ReactDOM. When the state of an object changes, React updates the virtual DOM, compares it with the previous virtual DOM, and calculates the most efficient way to update the real DOM.

### 8. Explain the lifecycle methods in React.

**Answer:**
React components have several lifecycle methods that you can override to run code at particular times in the process. The main phases are:
- **Mounting**: When a component is being inserted into the DOM.
  - `constructor()`
  - `static getDerivedStateFromProps()`
  - `render()`
  - `componentDidMount()`
  
- **Updating**: When a component is being re-rendered as a result of changes to either props or state.
  - `static getDerivedStateFromProps()`
  - `shouldComponentUpdate()`
  - `render()`
  - `getSnapshotBeforeUpdate()`
  - `componentDidUpdate()`

- **Unmounting**: When a component is being removed from the DOM.
  - `componentWillUnmount()`

### 9. What is the difference between controlled and uncontrolled components?

**Answer:**
- **Controlled Components**: Components that have their state controlled by React. The state is updated via `setState()` and the input value is driven by state.
  ```javascript
  import React, { useState } from 'react';

  function ControlledComponent() {
    const [value, setValue] = useState('');

    const handleChange = (event) => {
      setValue(event.target.value);
    };

    return (
      <input 
        type="text" 
        value={value} 
        onChange={handleChange} 
      />
    );
  }
  ```

- **Uncontrolled Components**: Components that store their own state internally. You access their current values using refs.
  ```javascript
  import React, { useRef } from 'react';

  function UncontrolledComponent() {
    const inputRef = useRef(null);

    const handleSubmit = () => {
      alert(inputRef.current.value);
    };

    return (
      <div>
        <input 
          type="text" 
          ref={inputRef} 
        />
        <button onClick={handleSubmit}>Submit</button>
      </div>
    );
  }
  ```

### 10. What are hooks in React?

**Answer:**
Hooks are a new addition to React (introduced in version 16.8) that allow you to use state and other React features without writing a class. The most commonly used hooks are:
- `useState()`: Allows you to add state to function components.
- `useEffect()`: Lets you perform side effects in function components (similar to `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`).
- `useContext()`: Accepts a context object and returns the current context value.

Example of `useState`:
```javascript
import React, { useState } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### 11. What are Higher-Order Components (HOCs) in React?

**Answer:**
Higher-Order Components (HOCs) are functions that take a component and return a new component. They allow for reusability of component logic by wrapping another component. HOCs are a pattern for sharing common functionality between components without repeating code.

Example:
```javascript
function withLogging(WrappedComponent) {
  return class extends React.Component {
    componentDidMount() {
      console.log('Component Mounted');
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
}
```

### 12. What is the purpose of keys in React?

**Answer:**
Keys are used in React to identify which items in a list have changed, been added, or removed. They help React efficiently update and render only the items that need to be changed. Each key should be a unique identifier within its siblings to ensure React can keep track of each element.

Example:
```javascript
const listItems = items.map((item) =>
  <li key={item.id}>{item.name}</li>
);
```

### 13. What is the difference between `useEffect` and `useLayoutEffect`?

**Answer:**
- **`useEffect`**: Runs after the render is committed to the screen. It is useful for operations that do not need to block the browser paint, such as fetching data or setting up subscriptions.
  
  ```javascript
  useEffect(() => {
    console.log('Component did mount or update');
  }, []);
  ```

- **`useLayoutEffect`**: Runs synchronously after all DOM mutations. It is useful for operations that need to read the layout from the DOM and synchronously re-render, such as measuring or setting up animations.

  ```javascript
  useLayoutEffect(() => {
    console.log('Component did layout');
  }, []);
  ```

### 14. How can you optimize a React application?

**Answer:**
- **Use the Production Build**: Ensure that you build your React app for production, which minifies and optimizes the code.
- **Use React.memo**: Prevents unnecessary re-renders of functional components by memoizing the rendered output.
- **Code Splitting**: Use dynamic `import()` and React.lazy to split code into smaller chunks.
- **Use `PureComponent` and `React.memo`**: Optimize class and functional components by preventing unnecessary re-renders.
- **Avoid Inline Functions**: Declare functions outside of the render method to avoid unnecessary re-creations.
- **Optimize State Management**: Keep state local where necessary and avoid redundant state updates.
- **Use `useCallback` and `useMemo`**: Optimize expensive calculations and functions by memoizing them.

### 15. What is the Context API and how is it used?

**Answer:**
The Context API allows you to pass data through the component tree without having to pass props down manually at every level. It is useful for global state management such as themes or user authentication.

Example:
```javascript
const ThemeContext = React.createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <ThemeContext.Consumer>
      {theme => <div>The theme is {theme}</div>}
    </ThemeContext.Consumer>
  );
}
```

### 16. What are fragments and why are they used in React?

**Answer:**
Fragments are a way to group multiple elements without adding an extra node to the DOM. They allow you to return multiple elements from a component’s render method.

Example:
```javascript
function MyComponent() {
  return (
    <React.Fragment>
      <h1>Title</h1>
      <p>Description</p>
    </React.Fragment>
  );
}
```
You can also use the shorthand syntax:
```javascript
function MyComponent() {
  return (
    <>
      <h1>Title</h1>
      <p>Description</p>
    </>
  );
}
```

### 17. What is prop drilling and how can it be avoided?

**Answer:**
Prop drilling is the process of passing data from a parent component to a deeply nested child component through multiple intermediate components. It can make the code harder to maintain and understand.

It can be avoided using:
- **Context API**: Allows you to pass data directly to a deeply nested component.
- **State Management Libraries**: Libraries like Redux or MobX can manage state globally and pass it down to components without prop drilling.

### 18. How do you handle forms in React?

**Answer:**
Handling forms in React typically involves managing the form state and handling form submission.

Example:
```javascript
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: '' };
  }

  handleChange = (event) => {
    this.setState({ value: event.target.value });
  }

  handleSubmit = (event) => {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### 19. What is Redux and how does it work with React?

**Answer:**
Redux is a state management library that helps manage application state in a predictable way. It works with React by providing a global state that can be accessed and updated from any component.

Redux concepts:
- **Store**: Holds the state of the application.
- **Actions**: Plain objects that describe the change in the state.
- **Reducers**: Functions that specify how the state changes in response to an action.

Example:
```javascript
// Action
const increment = () => ({ type: 'INCREMENT' });

// Reducer
const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    default:
      return state;
  }
};

// Store
const store = createStore(counter);

// Usage in a React component
store.subscribe(() => console.log(store.getState()));
store.dispatch(increment());
```

### 20. What is the use of `useReducer` hook?

**Answer:**
The `useReducer` hook is an alternative to `useState` for managing complex state logic in React components. It is particularly useful for managing state transitions that involve multiple actions.

Example:
```javascript
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}
```

### 21. What is the difference between `componentDidMount` and `componentDidUpdate`?

**Answer:**
- **`componentDidMount`**: This lifecycle method is invoked immediately after a component is mounted (inserted into the tree). It is typically used for initializing data (e.g., fetching data from an API).
  ```javascript
  componentDidMount() {
    // Code to run after the component is mounted
  }
  ```

- **`componentDidUpdate`**: This lifecycle method is invoked immediately after updating occurs. It is not called for the initial render. It is typically used for performing operations based on changes in props or state.
  ```javascript
  componentDidUpdate(prevProps, prevState) {
    // Code to run after the component updates
    if (this.props.someValue !== prevProps.someValue) {
      // Perform some operation
    }
  }
  ```

### 22. What is React Router, and how do you implement routing in a React application?

**Answer:**
React Router is a library for handling routing in React applications. It allows you to create routes to navigate between different components.

Example:
```javascript
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/home" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
        <Route path="/" component={Home} />
      </Switch>
    </Router>
  );
}
```

### 23. How does `shouldComponentUpdate` work, and why would you use it?

**Answer:**
`shouldComponentUpdate` is a lifecycle method that determines whether a component should re-render or not. By default, it returns `true`, but you can override it to return `false` to prevent re-rendering when there are no changes in state or props.

Example:
```javascript
shouldComponentUpdate(nextProps, nextState) {
  if (this.props.value !== nextProps.value) {
    return true;
  }
  return false;
}
```

### 24. What are error boundaries in React?

**Answer:**
Error boundaries are components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed. They do not catch errors inside event handlers.

Example:
```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    // Log the error to an error reporting service
    console.log(error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
```

### 25. What is the difference between `createRef` and `useRef`?

**Answer:**
- **`createRef`**: Used in class components to create a reference to a DOM element or a React element.
  ```javascript
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      this.myRef = React.createRef();
    }

    render() {
      return <div ref={this.myRef} />;
    }
  }
  ```

- **`useRef`**: Used in functional components to create a reference to a DOM element or a React element.
  ```javascript
  function MyComponent() {
    const myRef = React.useRef(null);

    return <div ref={myRef} />;
  }
  ```

### 26. What is a custom hook, and how do you create one?

**Answer:**
A custom hook is a function that starts with `use` and allows you to extract and reuse logic in functional components. Custom hooks let you use state and other hooks.

Example:
```javascript
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}
```

### 27. What is the difference between `React.memo` and `useMemo`?

**Answer:**
- **`React.memo`**: A higher-order component that memoizes the rendered output of a functional component, preventing unnecessary re-renders when props have not changed.
  ```javascript
  const MyComponent = React.memo((props) => {
    return <div>{props.value}</div>;
  });
  ```

- **`useMemo`**: A hook that memoizes the result of a function call, preventing expensive calculations on every render.
  ```javascript
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
  ```

### 28. How do you handle side effects in functional components?

**Answer:**
Side effects in functional components are handled using the `useEffect` hook. It allows you to perform side effects such as data fetching, subscriptions, or manually changing the DOM.

Example:
```javascript
import { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    // Perform a side effect
    const subscription = someAPI.subscribe();
    return () => {
      // Cleanup
      subscription.unsubscribe();
    };
  }, []); // Empty array means this effect runs once on mount and cleanup on unmount
}
```

### 29. What is the purpose of the `useContext` hook?

**Answer:**
The `useContext` hook allows you to use the context value directly in a functional component without the need for a Consumer component. It provides a way to access the nearest current value of a context.

Example:
```javascript
const MyContext = React.createContext();

function MyComponent() {
  const contextValue = useContext(MyContext);

  return <div>{contextValue}</div>;
}
```

### 30. How can you lazy load a component in React?

**Answer:**
Lazy loading a component in React is done using `React.lazy` and `Suspense`. This allows components to be loaded asynchronously when they are needed.

Example:
```javascript
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./LazyComponent'));

function App() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}
```

### 31. How do you handle conditional rendering in React?

**Answer:**
Conditional rendering in React can be handled using JavaScript conditional statements like `if`, ternary operators, or logical `&&`.

Examples:
- **Using `if` statements**:
  ```javascript
  function MyComponent(props) {
    if (props.isLoggedIn) {
      return <UserDashboard />;
    } else {
      return <Login />;
    }
  }
  ```

- **Using ternary operator**:
  ```javascript
  function MyComponent(props) {
    return (
      props.isLoggedIn ? <UserDashboard /> : <Login />
    );
  }
  ```

- **Using logical `&&`**:
  ```javascript
  function MyComponent(props) {
    return (
      <div>
        {props.isLoggedIn && <UserDashboard />}
        {!props.isLoggedIn && <Login />}
      </div>
    );
  }
  ```

### 32. What is the difference between `useEffect` and `useLayoutEffect` regarding execution timing?

**Answer:**
- **`useEffect`**: Runs after the render is committed to the screen. This means it executes after the paint, making it suitable for tasks that do not block the browser paint, like data fetching or subscriptions.
  ```javascript
  useEffect(() => {
    // Code that runs after render
  }, []);
  ```

- **`useLayoutEffect`**: Runs synchronously after all DOM mutations and before the browser has painted. This means it executes before the paint, making it suitable for tasks that need to read or modify the DOM and do not want to cause flickering.
  ```javascript
  useLayoutEffect(() => {
    // Code that runs before paint
  }, []);
  ```

### 33. What is the `useRef` hook, and what are its use cases?

**Answer:**
The `useRef` hook creates a mutable object which persists for the lifetime of the component. It can be used for:
- Accessing and interacting with a DOM element directly.
- Storing a mutable value that does not trigger re-renders when updated.
- Keeping a reference to a value across renders.

Example:
```javascript
function MyComponent() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

### 34. What is the purpose of `React.StrictMode`?

**Answer:**
`React.StrictMode` is a tool for highlighting potential problems in an application. It does not render any visible UI but activates additional checks and warnings for its descendants. It helps detect unexpected side effects, legacy API usage, and other potential issues.

Example:
```javascript
<React.StrictMode>
  <App />
</React.StrictMode>
```

### 35. How can you implement context with a custom hook in React?

**Answer:**
You can implement context with a custom hook by creating a context and then using a custom hook to provide and consume the context value.

Example:
```javascript
const MyContext = React.createContext();

function useMyContext() {
  const context = useContext(MyContext);
  if (!context) {
    throw new Error('useMyContext must be used within a MyProvider');
  }
  return context;
}

function MyProvider({ children }) {
  const value = { /* some value */ };

  return (
    <MyContext.Provider value={value}>
      {children}
    </MyContext.Provider>
  );
}

function MyComponent() {
  const context = useMyContext();
  return <div>{context.someValue}</div>;
}
```

### 36. How can you optimize performance when rendering lists in React?

**Answer:**
- **Use `key` props**: Ensure each list item has a unique key to help React identify changes.
- **Memoization**: Use `React.memo` to prevent unnecessary re-renders of list items.
- **Windowing/Virtualization**: Use libraries like `react-window` or `react-virtualized` to render only visible items in large lists.
- **Avoid Inline Functions**: Declare functions outside of the render method to avoid unnecessary re-creations.
- **Use `shouldComponentUpdate` or `PureComponent`**: Optimize class components by preventing unnecessary re-renders.

### 37. What is the significance of the `key` prop in React?

**Answer:**
The `key` prop helps React identify which items have changed, are added, or are removed. It must be unique among siblings and is used to optimize the rendering process by efficiently updating the list items.

Example:
```javascript
const listItems = items.map((item) =>
  <li key={item.id}>{item.name}</li>
);
```

### 38. How do you manage state in a React application using `useReducer`?

**Answer:**
`useReducer` is used for managing complex state logic. It takes a reducer function and an initial state as arguments and returns the current state and a dispatch function.

Example:
```javascript
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}
```

### 39. What is the role of the `setState` callback in class components?

**Answer:**
The `setState` callback function is an optional second argument that is executed once `setState` has finished and the component has re-rendered. It is useful for executing code after the state has been updated.

Example:
```javascript
this.setState({ count: this.state.count + 1 }, () => {
  console.log('State has been updated');
});
```

### 40. How do you handle asynchronous operations in React?

**Answer:**
Asynchronous operations in React are typically handled using:
- **Promises**: Use `.then()` and `.catch()` to handle asynchronous operations.
- **async/await**: Write asynchronous code in a more synchronous manner.
- **useEffect**: Perform side effects, such as data fetching, within this hook.

Example:
```javascript
import { useEffect, useState } from 'react';

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    async function fetchData() {
      const response = await fetch('https://api.example.com/data');
      const result = await response.json();
      setData(result);
    }
    fetchData();
  }, []); // Empty array means this effect runs once on mount

  return (
    <div>
      {data ? <div>{data.name}</div> : <div>Loading...</div>}
    </div>
  );
}
```

### 41. What is PropTypes and how do you use it in React?

**Answer:**
PropTypes is a mechanism to ensure that components receive props of the correct type. It helps in catching bugs by validating the types of props passed to a component.

Example:
```javascript
import PropTypes from 'prop-types';

function MyComponent({ name, age }) {
  return (
    <div>
      <h1>{name}</h1>
      <p>{age}</p>
    </div>
  );
}

MyComponent.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
};
```

### 42. How do you handle events in React?

**Answer:**
Event handling in React is similar to handling events in plain HTML but with some syntactic differences. React events are named using camelCase and you pass a function as the event handler.

Example:
```javascript
function MyComponent() {
  function handleClick() {
    alert('Button clicked!');
  }

  return (
    <button onClick={handleClick}>Click me</button>
  );
}
```

### 43. What is the purpose of `React.forwardRef`?

**Answer:**
`React.forwardRef` is used to pass refs to child components. This is useful for accessing the DOM node of child components or integrating with third-party libraries.

Example:
```javascript
const MyInput = React.forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));

function ParentComponent() {
  const inputRef = React.createRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <MyInput ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

### 44. How do you implement code splitting in a React application?

**Answer:**
Code splitting in React can be implemented using dynamic `import()` and React.lazy for lazy loading components, and `React.Suspense` for fallback UI during loading.

Example:
```javascript
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./LazyComponent'));

function App() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}
```

### 45. What is the significance of `defaultProps` in React?

**Answer:**
`defaultProps` allows you to define default values for props in a component. It ensures that the component has default values for props if they are not provided by the parent component.

Example:
```javascript
function MyComponent({ name }) {
  return <div>{name}</div>;
}

MyComponent.defaultProps = {
  name: 'Default Name',
};
```

### 46. How do you pass data between sibling components in React?

**Answer:**
Data between sibling components can be passed through their common parent component. The parent holds the state and passes data and callbacks as props to the sibling components.

Example:
```javascript
function ParentComponent() {
  const [data, setData] = useState('');

  return (
    <div>
      <SiblingOne setData={setData} />
      <SiblingTwo data={data} />
    </div>
  );
}

function SiblingOne({ setData }) {
  return (
    <input
      type="text"
      onChange={(e) => setData(e.target.value)}
    />
  );
}

function SiblingTwo({ data }) {
  return <div>{data}</div>;
}
```

### 47. What are synthetic events in React?

**Answer:**
Synthetic events in React are cross-browser wrappers around native events. They provide consistent behavior across different browsers and have the same interface as native events.

Example:
```javascript
function MyComponent() {
  function handleClick(event) {
    console.log(event.nativeEvent); // Native browser event
    console.log(event); // Synthetic event
  }

  return (
    <button onClick={handleClick}>Click me</button>
  );
}
```

### 48. How do you handle errors in React components?

**Answer:**
Errors in React components can be handled using Error Boundaries. These are components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI.

Example:
```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Log error information
    console.error(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

function MyComponent() {
  // Component code that might throw an error
}
```

### 49. How do you memoize a function in React?

**Answer:**
In React, functions can be memoized using the `useCallback` hook, which returns a memoized version of the callback that only changes if one of the dependencies has changed.

Example:
```javascript
function MyComponent() {
  const [count, setCount] = useState(0);

  const memoizedCallback = useCallback(() => {
    console.log('Callback called with count:', count);
  }, [count]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={memoizedCallback}>Call Memoized Callback</button>
    </div>
  );
}
```

### 50. What is the purpose of the `useImperativeHandle` hook?

**Answer:**
The `useImperativeHandle` hook customizes the instance value that is exposed when using `ref` in parent components. It allows you to control what is returned when a ref is accessed.

Example:
```javascript
const FancyInput = React.forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
  }));

  return <input ref={inputRef} />;
});

function ParentComponent() {
  const ref = useRef();

  return (
    <div>
      <FancyInput ref={ref} />
      <button onClick={() => ref.current.focus()}>Focus Input</button>
    </div>
  );
}
```

### 51. How do you handle form submission in React?

**Answer:**
Form submission in React is handled by defining an `onSubmit` event handler for the form element, which will be called when the form is submitted.

Example:
```javascript
import React, { useState } from 'react';

function MyForm() {
  const [value, setValue] = useState('');

  const handleChange = (event) => {
    setValue(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert('Form submitted with value: ' + value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text" 
        value={value} 
        onChange={handleChange} 
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 52. How do you handle state with multiple inputs in a form?

**Answer:**
You can handle state with multiple inputs by storing the form data in a single state object and updating the state for each input using a dynamic key.

Example:
```javascript
import React, { useState } from 'react';

function MyForm() {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: ''
  });

  const handleChange = (event) => {
    const { name, value } = event.target;
    setFormData({
      ...formData,
      [name]: value
    });
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`First Name: ${formData.firstName}, Last Name: ${formData.lastName}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="firstName"
        value={formData.firstName}
        onChange={handleChange}
      />
      <input
        type="text"
        name="lastName"
        value={formData.lastName}
        onChange={handleChange}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 53. How do you optimize a React application for performance?

**Answer:**
Several techniques can be used to optimize a React application for performance, including:
- **Using React.memo** to memoize functional components.
- **Using `useMemo` and `useCallback`** to memoize expensive calculations and functions.
- **Code splitting** using `React.lazy` and `Suspense`.
- **Avoiding unnecessary re-renders** by using `PureComponent` or `shouldComponentUpdate` in class components.
- **Windowing/virtualization** for large lists using libraries like `react-window`.

### 55. What is the purpose of `React.StrictMode`?

**Answer:**
`React.StrictMode` is a wrapper component that helps highlight potential problems in an application. It does not render any visible UI but activates additional checks and warnings for its descendants. It helps with identifying unsafe lifecycles, legacy API usage, and more.

Example:
```javascript
import React from 'react';

function App() {
  return (
    <React.StrictMode>
      <MyComponent />
    </React.StrictMode>
  );
}
```

### 54. How do you fetch data from an API in React?

**Answer:**
Data can be fetched from an API in React using the `useEffect` hook along with the `fetch` API.

Example:
```javascript
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []);

  if (!data) {
    return <div>Loading...</div>;
  }

  return (
    <div>
      <h1>Data from API:</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}
```

### 55. How do you implement routing in a React application?

**Answer:**
Routing in a React application can be implemented using the `react-router-dom` library.

Example:
```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom';

function Home() {
  return <h1>Home</h1>;
}

function About() {
  return <h1>About</h1>;
}

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
  );
}

export default App;
```

### 56. How do you handle side effects in React?

**Answer:**
Side effects in React can be handled using the `useEffect` hook. This hook allows you to perform side effects in function components.

Example:
```javascript
import React, { useEffect, useState } from 'react';

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Fetch data or perform other side effects here
    fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // Empty array means this effect runs once on mount

  return (
    <div>
      {data ? <div>{data}</div> : <div>Loading...</div>}
    </div>
  );
}
```

### 57. How do you manage global state in a React application?

**Answer:**
Global state in a React application can be managed using context and the `useContext` hook.

Example:
```javascript
import React, { createContext, useContext, useState } from 'react';

const MyContext = createContext();

function MyProvider({ children }) {
  const [state, setState] = useState('some value');

  return (
    <MyContext.Provider value={{ state, setState }}>
      {children}
    </MyContext.Provider>
  );
}

function MyComponent() {
  const { state, setState } = useContext(MyContext);

  return (
    <div>
      <p>Global state: {state}</p>
      <button onClick={() => setState('new value')}>Change State</button>
    </div>
  );
}

function App() {
  return (
    <MyProvider>
      <MyComponent />
    </MyProvider>
  );
}

export default App;
```
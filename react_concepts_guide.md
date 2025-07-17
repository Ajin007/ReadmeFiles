
# **React Concepts Guide**

## **1. Basic React Concepts**

### **What is React?**

React is a JavaScript library for building user interfaces (UIs), particularly single-page applications (SPAs). React enables developers to build reusable components and manage the UI in a declarative way, making it easier to create dynamic and interactive applications.

### **Core Concepts of React**

#### **1. Components**

A React component is a JavaScript function or class that accepts inputs (called "props") and returns a React element that describes what should appear on the UI.

```jsx
import React from 'react';

function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

export default Greeting;
```

Components can be:
- **Function Components**: Simple functions that return JSX.
- **Class Components**: Components created using JavaScript classes.

#### **2. JSX (JavaScript XML)**

JSX is a syntax extension for JavaScript. It allows you to write HTML-like structures in your JavaScript code. React components use JSX to describe what the UI should look like.

```jsx
const element = <h1>Hello, world!</h1>;
```

Note: JSX gets transpiled to `React.createElement()` calls, so it is not exactly HTML.

#### **3. State and Props**

- **Props**: Short for "properties," these are inputs to a React component. They are read-only and passed from parent to child components.

  ```jsx
  <Greeting name="John" />
  ```

- **State**: A way to store data that can change over time in a component. State is mutable and used for interactive components.

  ```jsx
  import React, { useState } from 'react';

  function Counter() {
    const [count, setCount] = useState(0); // Initial state set to 0

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>Click me</button>
      </div>
    );
  }

  export default Counter;
  ```

#### **4. Lifecycle Methods (Class Components)**

In class components, lifecycle methods allow you to perform actions at different points in a component's life cycle.

- **componentDidMount**: Runs after the component is mounted.
- **componentDidUpdate**: Runs after a component is updated.
- **componentWillUnmount**: Runs before the component is unmounted.

```jsx
class MyComponent extends React.Component {
  componentDidMount() {
    console.log('Component Mounted');
  }

  render() {
    return <h1>Hello, World!</h1>;
  }
}
```

#### **5. Hooks (Function Components)**

React hooks allow you to use state and lifecycle features in function components.

- **useState**: Manages state.
- **useEffect**: Performs side-effects (e.g., fetching data, DOM manipulation).

```jsx
import { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds((prev) => prev + 1), 1000);
    return () => clearInterval(interval); // Cleanup when component unmounts
  }, []); // Empty dependency array means effect runs once when component mounts

  return <p>Timer: {seconds} seconds</p>;
}
```

---

## **2. React Hooks**

### **2.1 useState Hook**

The `useState` hook is used to add state to function components.

#### **Example:**

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Initial state set to 0

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### **2.2 useEffect Hook**

The `useEffect` hook is used to perform side effects in function components (e.g., data fetching, DOM manipulation).

#### **Example:**

```jsx
import { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => setSeconds((prev) => prev + 1), 1000);
    return () => clearInterval(interval); // Cleanup when component unmounts
  }, []); // Empty dependency array means effect runs once when component mounts

  return <p>Timer: {seconds} seconds</p>;
}
```

### **2.3 useContext Hook**

The `useContext` hook allows you to consume context data directly inside a function component.

#### **Example:**

```jsx
import { useContext } from 'react';

// Create a context
const ThemeContext = React.createContext('light');

function ThemedComponent() {
  const theme = useContext(ThemeContext); // Consume the context value

  return <div>The current theme is {theme}</div>;
}
```

---

## **3. Debugging React**

### **3.1 React Developer Tools**

React Developer Tools is a browser extension that allows you to inspect the React component tree, view props and state, and track re-renders.

#### **Steps to use React Developer Tools**:
1. Install the [React Developer Tools extension](https://reactjs.org/blog/2019/08/15/new-react-devtools.html) for Chrome or Firefox.
2. Open the developer tools (`Ctrl + Shift + I`).
3. In the "React" tab, you'll see the component tree, props, and state.

### **3.2 `console.log()` for Debugging**

Use `console.log()` to log values and inspect state or props during execution.

```jsx
function MyComponent() {
  const [count, setCount] = useState(0);

  console.log('Count value:', count); // Debugging state

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### **3.3 `debugger` Statement**

Use the `debugger` statement to pause execution and inspect variables.

```jsx
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    debugger; // Pauses execution
    const interval = setInterval(() => setSeconds((prev) => prev + 1), 1000);
    return () => clearInterval(interval);
  }, []);

  return <p>Timer: {seconds} seconds</p>;
}
```

### **3.4 Tracking Re-renders**

Use `console.log()` or **React Developer Tools** to inspect when a component re-renders.

```jsx
function MyComponent() {
  console.log('Component rendered');

  return <div>Hello World</div>;
}
```

---

## **4. React Testing**

### **4.1 Testing with Jest**

Jest is a testing framework commonly used with React. It's used to run unit tests and mock functions.

#### **Running Tests**:
1. **Run all tests**:
   ```bash
   npm test
   ```

2. **Run tests with coverage**:
   ```bash
   npm test -- --coverage
   ```

#### **Example Test**:

```jsx
import { render, screen } from '@testing-library/react';
import MyComponent from './MyComponent';

test('renders MyComponent', () => {
  render(<MyComponent />);
  const linkElement = screen.getByText(/Hello World/i);
  expect(linkElement).toBeInTheDocument();
});
```

### **4.2 Mocking API Calls in Jest**

You can mock API calls using `jest.mock()`.

```jsx
import { render, screen } from '@testing-library/react';
import { fetchData } from './api'; // Mocked API function
import DataComponent from './DataComponent';

jest.mock('./api'); // Mocking the module

test('fetches and displays data', async () => {
  fetchData.mockResolvedValue({ data: 'Test Data' });

  render(<DataComponent />);
  const dataElement = await screen.findByText(/Test Data/i);
  expect(dataElement).toBeInTheDocument();
});
```

---

## **5. Advanced React Concepts**

### **5.1 React Context API**

React's Context API allows you to share values between components without passing props down manually.

#### **Creating Context**:

```jsx
const ThemeContext = React.createContext('light'); // Default value

function ThemedComponent() {
  const theme = useContext(ThemeContext); // Consume the context value
  return <div>The current theme is {theme}</div>;
}
```

### **5.2 Higher-Order Components (HOCs)**

An HOC is a function that takes a component and returns a new component with additional props or behavior.

```jsx
function withTitle(Component) {
  return function WrappedComponent(props) {
    return (
      <div>
        <h1>Title</h1>
        <Component {...props} />
      </div>
    );
  };
}
```

### **5.3 Render Props**

Render props allow you to share code between components using a prop that is a function.

```jsx
class MouseTracker extends React.Component {
  state = { x: 0, y: 0 };

  handleMouseMove = (event) => {
    this.setState({ x: event.clientX, y: event.clientY });
  };

  render() {
    return (
      <div onMouseMove={this.handleMouseMove}>
        {this.props.render(this.state)}
      </div>
    );
  }
}

// Usage
<MouseTracker render={({ x, y }) => <h1>Mouse Position: {x}, {y}</h1>} />
```

### **5.4 Code Splitting**

Code splitting improves performance by loading only the required JavaScript chunks.

```jsx
import { lazy, Suspense } from 'react';

const MyComponent = lazy(() => import('./MyComponent'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <MyComponent />
    </Suspense>
  );
}
```

### **5.5 Error Boundaries**

Error boundaries catch JavaScript errors anywhere in their child component tree and log those errors.

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
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

---

## **6. Conclusion**

This guide covered:
- **Basic React Concepts**: Components, JSX, State, and Props.
- **Event Handling**: How to handle user input and actions.
- **React Hooks**: `useState`, `useEffect`, `useContext`, `useRef`, and custom hooks.
- **Debugging**: Using `console.log()`, React Developer Tools, and `debugger`.
- **Testing**: Using Jest and React Testing Library for unit tests and mocking.
- **Advanced Concepts**: Context API, HOCs, Render Props, Error Boundaries, and Performance Optimization.

By mastering these concepts, you'll be well on your way to becoming proficient in React development.

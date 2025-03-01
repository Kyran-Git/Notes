# React.js Notes

## Table of Contents
- [Introduction to React](#introduction-to-react)
- [Setting Up a React Project](#setting-up-a-react-project)
- [JSX Syntax](#jsx-syntax)
- [Components](#components)
- [Props](#props)
- [State](#state)
- [Hooks](#hooks)
- [Event Handling](#event-handling)
- [Conditional Rendering](#conditional-rendering)
- [Lists and Keys](#lists-and-keys)
- [Forms](#forms)
- [Context API](#context-api)
- [React Router](#react-router)
- [Performance Optimization](#performance-optimization)
- [Error Boundaries](#error-boundaries)
- [Testing React Applications](#testing-react-applications)

## Introduction to React

React is a JavaScript library for building user interfaces, particularly single-page applications. It was developed by Facebook and is maintained by Facebook and a community of individual developers and companies.

**Key Features:**
- **Component-Based Architecture**: Build encapsulated components that manage their own state
- **Declarative UI**: Design simple views for each state in your application
- **Virtual DOM**: Efficiently update and render components when data changes
- **One-way Data Flow**: Data flows down from parent to child components
- **JSX**: JavaScript syntax extension that allows HTML-like code in JavaScript

## Setting Up a React Project

### Using Create React App

```bash
# Install Create React App globally
npm install -g create-react-app

# Create a new React project
npx create-react-app my-app

# Navigate to project directory
cd my-app

# Start the development server
npm start
```

### Using Vite (Faster Alternative)

```bash
# Create a new React project with Vite
npm create vite@latest my-app -- --template react

# Navigate to project directory
cd my-app

# Install dependencies
npm install

# Start the development server
npm run dev
```

## JSX Syntax

JSX (JavaScript XML) allows you to write HTML-like code in JavaScript. It gets transformed into regular JavaScript at build time.

```jsx
// Basic JSX example
const element = <h1>Hello, world!</h1>;

// JSX with expressions
const name = "John";
const greeting = <h1>Hello, {name}!</h1>;

// JSX with attributes
const link = <a href="https://reactjs.org">React Website</a>;

// JSX with multiple elements needs a parent wrapper
const container = (
  <div>
    <h1>Title</h1>
    <p>Paragraph</p>
  </div>
);

// Self-closing tags
const image = <img src="image.jpg" alt="An image" />;
```

**JSX Rules:**
- All tags must be closed (either with closing tag or self-closing)
- Component names must start with a capital letter
- JavaScript expressions inside JSX must be wrapped in curly braces `{}`
- `class` attribute is written as `className`
- `for` attribute is written as `htmlFor`
- Inline styles are written as objects with camelCase properties

## Components

Components are the building blocks of React applications. They are reusable pieces of code that return React elements describing what should appear on the screen.

### Function Components

```jsx
// Simple function component
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Arrow function component
const Welcome = (props) => {
  return <h1>Hello, {props.name}</h1>;
};

// Usage
<Welcome name="Sara" />
```

### Class Components

```jsx
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

// Usage
<Welcome name="Sara" />
```

### Component Composition

```jsx
function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
```

## Props

Props (short for properties) are read-only inputs to components. They are passed from parent to child components.

```jsx
// Parent component passing props
function App() {
  return <Welcome name="Sara" age={25} isAdmin={true} />;
}

// Child component receiving props
function Welcome(props) {
  return (
    <div>
      <h1>Hello, {props.name}</h1>
      <p>Age: {props.age}</p>
      <p>Admin: {props.isAdmin ? 'Yes' : 'No'}</p>
    </div>
  );
}
```

### Destructuring Props

```jsx
function Welcome({ name, age, isAdmin }) {
  return (
    <div>
      <h1>Hello, {name}</h1>
      <p>Age: {age}</p>
      <p>Admin: {isAdmin ? 'Yes' : 'No'}</p>
    </div>
  );
}
```

### Default Props

```jsx
function Welcome({ name, age = 18, isAdmin = false }) {
  return (
    <div>
      <h1>Hello, {name}</h1>
      <p>Age: {age}</p>
      <p>Admin: {isAdmin ? 'Yes' : 'No'}</p>
    </div>
  );
}
```

## State

State is a built-in object that contains data or information about the component. Unlike props, state can be changed.

### State in Class Components

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

### State Updates May Be Asynchronous

```jsx
// Wrong way
this.setState({
  count: this.state.count + 1
});

// Correct way (using function form)
this.setState((prevState) => ({
  count: prevState.count + 1
}));
```

## Hooks

Hooks are functions that let you "hook into" React state and lifecycle features from function components.

### useState

```jsx
import React, { useState } from 'react';

function Counter() {
  // Declare a state variable 'count' with initial value 0
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
```

### useEffect

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    // This runs after every render
    const interval = setInterval(() => {
      setSeconds(seconds => seconds + 1);
    }, 1000);

    // Cleanup function (runs before component unmounts or before next effect)
    return () => clearInterval(interval);
  }, []); // Empty dependency array means this effect runs once on mount

  return <p>Seconds: {seconds}</p>;
}
```

### useContext

```jsx
import React, { createContext, useContext, useState } from 'react';

// Create a context
const ThemeContext = createContext('light');

function App() {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={theme}>
      <div>
        <ThemedButton />
        <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>
          Toggle Theme
        </button>
      </div>
    </ThemeContext.Provider>
  );
}

function ThemedButton() {
  // Use the context
  const theme = useContext(ThemeContext);
  
  return (
    <button style={{ 
      background: theme === 'light' ? '#fff' : '#333',
      color: theme === 'light' ? '#333' : '#fff'
    }}>
      I am styled based on the theme context!
    </button>
  );
}
```

### useReducer

```jsx
import React, { useReducer } from 'react';

// Reducer function
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: 0 };
    default:
      throw new Error();
  }
}

function Counter() {
  // useReducer returns current state and a dispatch function
  const [state, dispatch] = useReducer(counterReducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
      <button onClick={() => dispatch({ type: 'reset' })}>Reset</button>
    </div>
  );
}
```

### useRef

```jsx
import React, { useRef, useEffect } from 'react';

function TextInputWithFocusButton() {
  // Create a ref
  const inputRef = useRef(null);

  // Function to focus the input
  const focusInput = () => {
    inputRef.current.focus();
  };

  // Focus input on mount
  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

### useMemo

```jsx
import React, { useState, useMemo } from 'react';

function ExpensiveCalculation({ list }) {
  // This calculation will only run when the list changes
  const sortedList = useMemo(() => {
    console.log('Sorting list...');
    return [...list].sort((a, b) => a - b);
  }, [list]);

  return (
    <div>
      <p>Sorted List: {sortedList.join(', ')}</p>
    </div>
  );
}

function App() {
  const [numbers, setNumbers] = useState([10, 5, 3, 8, 2]);
  const [count, setCount] = useState(0);

  return (
    <div>
      <ExpensiveCalculation list={numbers} />
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### useCallback

```jsx
import React, { useState, useCallback } from 'react';

function ParentComponent() {
  const [count, setCount] = useState(0);
  
  // This function is memoized and only changes if dependencies change
  const handleClick = useCallback(() => {
    console.log(`Button clicked, count: ${count}`);
  }, [count]); // Recreate function when count changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}

// Child component that receives the callback
function ChildComponent({ onClick }) {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click me</button>;
}

// Optimize child component with React.memo
const MemoizedChildComponent = React.memo(ChildComponent);
```

### use (React 18+)

The `use` hook is a new addition in React 18+ that allows you to use resources like Promises directly in your components.

```jsx
import { use, Suspense } from 'react';

// Function that returns a promise
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('Data loaded!');
    }, 2000);
  });
}

// Create a resource
const dataPromise = fetchData();

function DataComponent() {
  // Use the promise directly in your component
  const data = use(dataPromise);
  
  return <div>{data}</div>;
}

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <DataComponent />
    </Suspense>
  );
}
```

## Event Handling

React events are named using camelCase and passed as functions rather than strings.

```jsx
function Button() {
  const handleClick = (e) => {
    e.preventDefault(); // Prevent default behavior
    console.log('Button clicked!');
  };

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

### Passing Arguments to Event Handlers

```jsx
function ItemList() {
  const handleItemClick = (id, e) => {
    console.log(`Item ${id} clicked`);
  };

  return (
    <ul>
      <li onClick={(e) => handleItemClick(1, e)}>Item 1</li>
      <li onClick={(e) => handleItemClick(2, e)}>Item 2</li>
    </ul>
  );
}
```

## Conditional Rendering

### Using if Statements

```jsx
function UserGreeting(props) {
  if (props.isLoggedIn) {
    return <h1>Welcome back!</h1>;
  }
  return <h1>Please sign in.</h1>;
}
```

### Using Ternary Operators

```jsx
function UserGreeting(props) {
  return (
    <h1>
      {props.isLoggedIn ? 'Welcome back!' : 'Please sign in'}
    </h1>
  );
}
```

### Using Logical && Operator

```jsx
function Notifications(props) {
  return (
    <div>
      <h1>Notifications</h1>
      {props.unreadMessages.length > 0 &&
        <p>You have {props.unreadMessages.length} unread messages.</p>
      }
    </div>
  );
}
```

## Lists and Keys

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Each list item needs a unique "key" prop
    <li key={number.toString()}>
      {number}
    </li>
  );

  return <ul>{listItems}</ul>;
}
```

### Keys

Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity.

```jsx
function TodoList(props) {
  return (
    <ul>
      {props.todos.map((todo) =>
        <li key={todo.id}>
          {todo.text}
        </li>
      )}
    </ul>
  );
}
```

## Forms

### Controlled Components

```jsx
import React, { useState } from 'react';

function NameForm() {
  const [name, setName] = useState('');

  const handleChange = (event) => {
    setName(event.target.value);
  };

  const handleSubmit = (event) => {
    alert('A name was submitted: ' + name);
    event.preventDefault();
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```

### Multiple Inputs

```jsx
import React, { useState } from 'react';

function ContactForm() {
  const [formData, setFormData] = useState({
    firstName: '',
    lastName: '',
    email: ''
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
    console.log('Form submitted:', formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          First Name:
          <input
            type="text"
            name="firstName"
            value={formData.firstName}
            onChange={handleChange}
          />
        </label>
      </div>
      <div>
        <label>
          Last Name:
          <input
            type="text"
            name="lastName"
            value={formData.lastName}
            onChange={handleChange}
          />
        </label>
      </div>
      <div>
        <label>
          Email:
          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={handleChange}
          />
        </label>
      </div>
      <button type="submit">Submit</button>
    </form>
  );
}
```

## Context API

Context provides a way to pass data through the component tree without having to pass props down manually at every level.

```jsx
import React, { createContext, useContext, useState } from 'react';

// Create a context with a default value
const ThemeContext = createContext('light');

// Provider component
function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(theme === 'light' ? 'dark' : 'light');
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Custom hook to use the theme context
function useTheme() {
  return useContext(ThemeContext);
}

// Component that uses the theme
function ThemedButton() {
  const { theme, toggleTheme } = useTheme();
  
  return (
    <button
      onClick={toggleTheme}
      style={{
        background: theme === 'light' ? '#fff' : '#333',
        color: theme === 'light' ? '#333' : '#fff',
        padding: '10px 15px',
        border: '1px solid #ccc',
        borderRadius: '4px'
      }}
    >
      Toggle Theme
    </button>
  );
}

// App component
function App() {
  return (
    <ThemeProvider>
      <div style={{ padding: '20px' }}>
        <h1>Context API Example</h1>
        <ThemedButton />
      </div>
    </ThemeProvider>
  );
}
```

## React Router

React Router is a standard library for routing in React applications.

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

// Components for different routes
function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Page</h2>;
}

function Contact() {
  return <h2>Contact Page</h2>;
}

// App with routing
function App() {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about">About</Link>
            </li>
            <li>
              <Link to="/contact">Contact</Link>
            </li>
          </ul>
        </nav>

        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}
```

### URL Parameters

```jsx
import React from 'react';
import { BrowserRouter, Routes, Route, Link, useParams } from 'react-router-dom';

// Component that uses URL parameters
function UserProfile() {
  // Get the userId from the URL
  const { userId } = useParams();
  
  return <h2>User Profile: {userId}</h2>;
}

function App() {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/users/1">User 1</Link>
            </li>
            <li>
              <Link to="/users/2">User 2</Link>
            </li>
          </ul>
        </nav>

        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/users/:userId" element={<UserProfile />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}
```

## Performance Optimization

### React.memo

```jsx
import React, { useState } from 'react';

// Regular component
function Button({ onClick, text }) {
  console.log(`${text} button rendered`);
  return <button onClick={onClick}>{text}</button>;
}

// Memoized component - only re-renders if props change
const MemoizedButton = React.memo(Button);

function App() {
  const [count, setCount] = useState(0);
  
  // This function is recreated on every render
  const incrementCount = () => setCount(count + 1);
  
  // This function reference remains stable
  const resetCount = React.useCallback(() => setCount(0), []);

  return (
    <div>
      <p>Count: {count}</p>
      {/* Will re-render on every parent render because incrementCount changes */}
      <MemoizedButton onClick={incrementCount} text="Increment" />
      {/* Will only re-render when resetCount changes (which is never) */}
      <MemoizedButton onClick={resetCount} text="Reset" />
    </div>
  );
}
```

### useMemo for Expensive Calculations

```jsx
import React, { useState, useMemo } from 'react';

function ExpensiveComponent({ data }) {
  // Expensive calculation memoized
  const processedData = useMemo(() => {
    console.log('Processing data...');
    // Simulate expensive operation
    return data.map(item => item * 2).filter(item => item > 10);
  }, [data]); // Only recalculate when data changes

  return (
    <div>
      <p>Processed items: {processedData.length}</p>
      <ul>
        {processedData.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
    </div>
  );
}
```

## Error Boundaries

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI.

```jsx
import React, { Component } from 'react';

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    console.error('Error caught by boundary:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

// Usage
function App() {
  return (
    <div>
      <ErrorBoundary>
        <MyComponent />
      </ErrorBoundary>
    </div>
  );
}
```

## Testing React Applications

### Testing with Jest and React Testing Library

```jsx
// Button.js
import React from 'react';

function Button({ onClick, text }) {
  return (
    <button onClick={onClick} data-testid="custom-button">
      {text}
    </button>
  );
}

export default Button;
```

```jsx
// Button.test.js
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import Button from './Button';

test('renders button with correct text', () => {
  render(<Button text="Click me" onClick={() => {}} />);
  const buttonElement = screen.getByTestId('custom-button');
  expect(buttonElement).toBeInTheDocument();
  expect(buttonElement.textContent).toBe('Click me');
});

test('calls onClick when button is clicked', () => {
  const handleClick = jest.fn();
  render(<Button text="Click me" onClick={handleClick} />);
  const buttonElement = screen.getByTestId('custom-button');
  
  fireEvent.click(buttonElement);
  
  expect(handleClick).toHaveBeenCalledTimes(1);
});
```

### Testing Asynchronous Code

```jsx
// UserData.js
import React, { useState, useEffect } from 'react';

function UserData({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchUser() {
      try {
        setLoading(true);
        const response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
        if (!response.ok) throw new Error('Failed to fetch');
        const data = await response.json();
        setUser(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchUser();
  }, [userId]);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  if (!user) return null;

  return (
    <div>
      <h2>{user.name}</h2>
      <p>Email: {user.email}</p>
      <p>Phone: {user.phone}</p>
    </div>
  );
}

export default UserData;
```

```jsx
// UserData.test.js
import React from 'react';
import { render, screen, waitFor } from '@testing-library/react';
import UserData from './UserData';

// Mock fetch
global.fetch = jest.fn();

test('displays user data after successful fetch', async () => {
  const mockUser = {
    id: 1,
    name: 'John Doe',
    email: 'john@example.com',
    phone: '123-456-7890'
  };

  // Mock successful response
  fetch.mockResolvedValueOnce({
    ok: true,
    json: async () => mockUser
  });

  render(<UserData userId={1} />);
  
  // Initially shows loading
  expect(screen.getByText('Loading...')).toBeInTheDocument();
  
  // Wait for user data to be displayed
  await waitFor(() => {
    expect(screen.getByText('John Doe')).toBeInTheDocument();
  });
  
  expect(screen.getByText('Email: john@example.com')).toBeInTheDocument();
  expect(screen.getByText('Phone: 123-456-7890')).toBeInTheDocument();
  
  // Verify fetch was called correctly
  expect(fetch).toHaveBeenCalledWith('https://jsonplaceholder.typicode.com/users/1');
});
```

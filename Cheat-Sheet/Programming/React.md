# React Cheat Sheet

## Introduction

**React** is a free, open-source JavaScript library for building user interfaces, created by **Jordan Walke** at **Facebook** and released in **2013**. React uses a **component-based architecture** — UIs are built from small, reusable pieces called components. React's **Virtual DOM** efficiently updates only what changes on the real page, making it fast. With the introduction of **Hooks** in React 16.8 (2019), functional components became the standard way to write React. React is used for web apps (react-dom), mobile apps (React Native), and static sites (Next.js). It is the most popular frontend library in the world.

---

## Table of Contents

1. [Basic Syntax & JSX](#basic-syntax--jsx)
2. [Components](#components)
3. [Props](#props)
4. [State — useState](#state--usestate)
5. [Event Handling](#event-handling)
6. [Conditional Rendering](#conditional-rendering)
7. [Lists & Keys](#lists--keys)
8. [Forms & Controlled Components](#forms--controlled-components)
9. [useEffect](#useeffect)
10. [useRef](#useref)
11. [useContext](#usecontext)
12. [useReducer](#usereducer)
13. [useMemo](#usememo)
14. [useCallback](#usecallback)
15. [Custom Hooks](#custom-hooks)
16. [Component Lifecycle (with Hooks)](#component-lifecycle-with-hooks)
17. [Fragments](#fragments)
18. [Portals](#portals)
19. [Error Boundaries](#error-boundaries)
20. [Lazy Loading & Suspense](#lazy-loading--suspense)
21. [Higher-Order Components](#higher-order-components)
22. [Render Props](#render-props)
23. [Compound Components](#compound-components)
24. [Forwarding Refs](#forwarding-refs)
25. [Context API (Full Pattern)](#context-api-full-pattern)
26. [Performance Optimization](#performance-optimization)
27. [React.memo](#reactmemo)
28. [Styling in React](#styling-in-react)
29. [React Router (v6)](#react-router-v6)
30. [Data Fetching Patterns](#data-fetching-patterns)
31. [TypeScript with React](#typescript-with-react)
32. [Testing React Components](#testing-react-components)
33. [Project Setup](#project-setup)
34. [Tips & Tricks](#tips--tricks)
35. [Best Practices](#best-practices)

---

## Basic Syntax & JSX

**Definition:** JSX is a syntax extension that looks like HTML inside JavaScript — Babel compiles it to `React.createElement()` calls.

### JSX Basics
**Definition:** JSX lets you write HTML-like markup inside JavaScript — must have one root element.
```jsx
// JSX looks like HTML but compiles to JavaScript
const element = <h1>Hello, World!</h1>;

// Must return one root element — use Fragment or wrapper div
function App() {
    return (
        <div>
            <h1>Hello</h1>
            <p>World</p>
        </div>
    );
}
```

### JSX Rules
**Definition:** JSX has specific syntax differences from HTML — follow these to avoid errors.
```jsx
// 1. Use className instead of class
<div className="container">

// 2. Use htmlFor instead of for
<label htmlFor="email">Email</label>

// 3. Self-close tags without children
<img src="photo.jpg" alt="photo" />
<input type="text" />
<br />

// 4. Use camelCase for attributes
<button onClick={handleClick} tabIndex={0}>

// 5. Expressions in curly braces {}
const name = "Dark";
<h1>Hello, {name}!</h1>
<p>2 + 2 = {2 + 2}</p>
<p>{condition ? "Yes" : "No"}</p>

// 6. Comments in JSX
<div>
    {/* This is a JSX comment */}
    <p>Content</p>
</div>

// 7. Style as object (camelCase properties)
<div style={{ color: "red", fontSize: "16px", marginTop: "8px" }}>

// 8. Boolean attributes
<input disabled />          // disabled={true}
<input disabled={false} />  // attribute omitted
```

### JSX Expressions
**Definition:** Use `{}` to embed any valid JavaScript expression inside JSX.
```jsx
const user = { name: "Dark", age: 25 };
const isLoggedIn = true;

function UserCard() {
    return (
        <div>
            <h2>{user.name}</h2>
            <p>Age: {user.age}</p>
            <p>Status: {isLoggedIn ? "Online" : "Offline"}</p>
            <p>Greeting: {"Hello ".repeat(3)}</p>
            {isLoggedIn && <button>Logout</button>}
        </div>
    );
}
```

---

## Components

**Definition:** Components are the building blocks of React — reusable, independent pieces of UI.

### Functional Component
**Definition:** A JavaScript function that returns JSX — the modern standard way to write components.
```jsx
// Simple functional component
function Greeting() {
    return <h1>Hello, World!</h1>;
}

// Arrow function (also common)
const Greeting = () => <h1>Hello, World!</h1>;

// With content
function UserCard({ name, age }) {
    return (
        <div className="card">
            <h2>{name}</h2>
            <p>Age: {age}</p>
        </div>
    );
}

// Export
export default Greeting;
export { UserCard };
```

### Component Composition
**Definition:** Build complex UIs by combining smaller components inside each other.
```jsx
function Avatar({ src, alt }) {
    return <img src={src} alt={alt} className="avatar" />;
}

function UserInfo({ user }) {
    return (
        <div className="user-info">
            <Avatar src={user.avatar} alt={user.name} />
            <h3>{user.name}</h3>
            <p>{user.email}</p>
        </div>
    );
}

function App() {
    const user = { name: "Dark", email: "dark@ex.com", avatar: "photo.jpg" };
    return (
        <main>
            <UserInfo user={user} />
        </main>
    );
}
```

### Children Prop
**Definition:** Components can receive nested JSX as `children` — makes components flexible wrappers.
```jsx
// Card accepts anything between its tags
function Card({ children, className = "" }) {
    return (
        <div className={`card ${className}`}>
            {children}
        </div>
    );
}

// Use it
function App() {
    return (
        <Card className="featured">
            <h2>Title</h2>
            <p>Some content inside the card.</p>
            <button>Read More</button>
        </Card>
    );
}
```

---

## Props

**Definition:** Props (properties) are how data flows from parent to child — read-only, never modify them.

### Basic Props
**Definition:** Pass data to child components as attributes — receive them as an object parameter.
```jsx
// Define component with props
function Welcome({ name, age, city = "Unknown" }) {   // Default value
    return (
        <div>
            <h1>Welcome, {name}!</h1>
            <p>Age: {age}</p>
            <p>City: {city}</p>
        </div>
    );
}

// Pass props from parent
function App() {
    return (
        <div>
            <Welcome name="Dark" age={25} city="Mumbai" />
            <Welcome name="Alice" age={30} />    {/* city defaults to "Unknown" */}
        </div>
    );
}
```

### Spread Props
**Definition:** Spread an object's properties as individual props — useful for passing props through layers.
```jsx
function Button({ label, ...rest }) {    // ...rest collects remaining props
    return <button {...rest}>{label}</button>;
}

// Pass many props at once
const buttonProps = { onClick: handleClick, disabled: false, type: "submit" };
<Button label="Submit" {...buttonProps} />

// All HTML button attributes supported automatically
<Button label="Click" onClick={fn} className="btn-primary" aria-label="Submit form" />
```

### Prop Types Validation
**Definition:** Validate prop types at runtime — helps catch bugs during development.
```jsx
import PropTypes from 'prop-types';

function UserCard({ name, age, email, isAdmin }) {
    return <div>{name}</div>;
}

UserCard.propTypes = {
    name:    PropTypes.string.isRequired,
    age:     PropTypes.number.isRequired,
    email:   PropTypes.string,
    isAdmin: PropTypes.bool,
    onClick: PropTypes.func,
    items:   PropTypes.arrayOf(PropTypes.string),
    user:    PropTypes.shape({
        id:   PropTypes.number,
        name: PropTypes.string
    })
};

UserCard.defaultProps = {
    email:   "",
    isAdmin: false
};
```

---

## State — useState

**Definition:** State is data that can change over time — when state changes, React re-renders the component.

### Basic useState
**Definition:** Declare state with `useState` — returns current value and a setter function.
```jsx
import { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);     // Initial value: 0

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={() => setCount(count + 1)}>+</button>
            <button onClick={() => setCount(count - 1)}>-</button>
            <button onClick={() => setCount(0)}>Reset</button>
        </div>
    );
}
```

### Functional Updates
**Definition:** When new state depends on old state, pass a function to the setter — avoids stale state bugs.
```jsx
function Counter() {
    const [count, setCount] = useState(0);

    // BAD — may use stale value in async context
    const increment = () => setCount(count + 1);

    // GOOD — always uses latest state value
    const increment = () => setCount(prev => prev + 1);
    const double    = () => setCount(prev => prev * 2);
    const reset     = () => setCount(0);

    return (
        <div>
            <p>{count}</p>
            <button onClick={increment}>+1</button>
            <button onClick={double}>×2</button>
            <button onClick={reset}>Reset</button>
        </div>
    );
}
```

### State with Objects & Arrays
**Definition:** Always create a new object/array when updating state — never mutate directly.
```jsx
function UserForm() {
    const [user, setUser] = useState({ name: "", email: "", age: 0 });
    const [items, setItems] = useState(["apple", "banana"]);

    // Update one field in object — spread to keep other fields
    const updateName = (e) =>
        setUser(prev => ({ ...prev, name: e.target.value }));

    // Add to array — spread existing + new item
    const addItem = (item) =>
        setItems(prev => [...prev, item]);

    // Remove from array — filter out
    const removeItem = (index) =>
        setItems(prev => prev.filter((_, i) => i !== index));

    // Update item in array — map to replace
    const updateItem = (index, newValue) =>
        setItems(prev => prev.map((item, i) => i === index ? newValue : item));

    return (
        <input value={user.name} onChange={updateName} />
    );
}
```

### Lazy Initial State
**Definition:** Pass a function to useState when initial state is expensive to compute — runs only once.
```jsx
// Expensive computation — runs every render
const [data, setData] = useState(expensiveComputation());

// Lazy initialization — only runs on first render
const [data, setData] = useState(() => expensiveComputation());
const [items, setItems] = useState(() => JSON.parse(localStorage.getItem('items') || '[]'));
```

---

## Event Handling

**Definition:** Attach event handlers to JSX elements using camelCase event names and function references.

### Basic Event Handlers
**Definition:** Pass a function (not a call) to event props — React handles event delegation.
```jsx
function EventDemo() {
    const handleClick  = () => console.log("Clicked!");
    const handleChange = (e) => console.log(e.target.value);
    const handleSubmit = (e) => {
        e.preventDefault();             // Prevent form page reload
        console.log("Submitted");
    };

    return (
        <div>
            {/* Pass function reference — NOT handleClick() */}
            <button onClick={handleClick}>Click Me</button>

            {/* Inline arrow function */}
            <button onClick={() => console.log("Inline")}>Inline</button>

            {/* With parameters — must wrap in arrow function */}
            <button onClick={() => handleDelete(item.id)}>Delete</button>

            <input onChange={handleChange} />
            <form onSubmit={handleSubmit}></form>
        </div>
    );
}
```

### Common Events
**Definition:** Frequently used React event handlers.
```jsx
// Mouse events
onClick         onDoubleClick     onMouseEnter
onMouseLeave    onMouseOver       onMouseOut
onMouseDown     onMouseUp         onMouseMove

// Keyboard events
onKeyDown       onKeyUp           onKeyPress

// Form events
onChange        onSubmit          onFocus
onBlur          onInput           onReset

// Clipboard events
onCopy          onCut             onPaste

// Touch events (mobile)
onTouchStart    onTouchMove       onTouchEnd

// Drag events
onDrag          onDragStart       onDragEnd
onDrop          onDragOver        onDragEnter

// Window events
onScroll        onWheel           onResize
```

### Event Object
**Definition:** The synthetic event object passed to every handler — wraps native browser events.
```jsx
function InputHandler() {
    const handleChange = (e) => {
        e.target.value          // Input value
        e.target.name           // Input name attribute
        e.target.checked        // Checkbox state
        e.target.type           // Input type
        e.preventDefault()      // Prevent default behavior
        e.stopPropagation()     // Stop event bubbling
    };

    const handleKeyDown = (e) => {
        if (e.key === 'Enter')    doSomething();
        if (e.key === 'Escape')   cancel();
        if (e.ctrlKey && e.key === 's') save();
        console.log(e.keyCode);  // Numeric key code
    };

    return <input onChange={handleChange} onKeyDown={handleKeyDown} />;
}
```

---

## Conditional Rendering

**Definition:** Render different UI based on conditions — React has no special template syntax, use JavaScript.

### if / else
**Definition:** Use regular JavaScript if/else outside the return statement.
```jsx
function Dashboard({ isLoggedIn, role }) {
    if (!isLoggedIn) {
        return <LoginPrompt />;
    }

    if (role === 'admin') {
        return <AdminDashboard />;
    }

    return <UserDashboard />;
}
```

### Ternary Operator
**Definition:** Compact inline conditional — renders one of two options.
```jsx
function UserStatus({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? <UserMenu /> : <LoginButton />}
            <p>{isLoggedIn ? "Welcome back!" : "Please log in"}</p>
        </div>
    );
}
```

### Short-circuit &&
**Definition:** Render something only when condition is true — nothing rendered when false.
```jsx
function Notifications({ count, isAdmin, error }) {
    return (
        <div>
            {count > 0 && <Badge count={count} />}
            {isAdmin && <AdminPanel />}
            {error && <ErrorMessage message={error} />}

            {/* CAREFUL: 0 is rendered! Use !! or > 0 */}
            {count > 0 && <p>{count} items</p>}  {/* Safe */}
            {!!count && <p>{count} items</p>}     {/* Also safe */}
        </div>
    );
}
```

### Nullish Coalescing
**Definition:** Render a fallback when value is null or undefined.
```jsx
function UserName({ user }) {
    return <h1>{user?.name ?? "Anonymous"}</h1>;
}
```

---

## Lists & Keys

**Definition:** Render arrays of elements using `.map()` — each element needs a unique `key` prop.

### Rendering Lists
**Definition:** Use `.map()` to transform data arrays into JSX arrays — always add `key`.
```jsx
function FruitList() {
    const fruits = ["Apple", "Banana", "Cherry"];

    return (
        <ul>
            {fruits.map((fruit, index) => (
                <li key={index}>{fruit}</li>
            ))}
        </ul>
    );
}

// Better — use unique ID as key when available
function UserList({ users }) {
    return (
        <ul>
            {users.map(user => (
                <li key={user.id}>
                    <strong>{user.name}</strong> — {user.email}
                </li>
            ))}
        </ul>
    );
}
```

### Key Rules
**Definition:** Keys help React identify which items changed — must be unique and stable.
```jsx
// BAD — index as key (causes bugs when list is reordered/filtered)
items.map((item, index) => <Item key={index} {...item} />)

// GOOD — stable unique ID from data
items.map(item => <Item key={item.id} {...item} />)

// GOOD — unique string
items.map(item => <Item key={item.slug} {...item} />)

// Keys are NOT passed as props — use a different prop name if needed
items.map(item => <Item key={item.id} itemId={item.id} {...item} />)
```

### Filter & Sort in Lists
**Definition:** Chain array methods before `.map()` to filter and sort data.
```jsx
function FilteredList({ items, filter, sortBy }) {
    const displayItems = items
        .filter(item => item.category === filter)
        .sort((a, b) => a[sortBy].localeCompare(b[sortBy]))
        .map(item => <ListItem key={item.id} item={item} />);

    return (
        <ul>
            {displayItems.length > 0
                ? displayItems
                : <li>No items found</li>
            }
        </ul>
    );
}
```

---

## Forms & Controlled Components

**Definition:** In controlled components, React state drives form values — every change updates state.

### Controlled Input
**Definition:** Bind input value to state — React owns the input value completely.
```jsx
function LoginForm() {
    const [email, setEmail]       = useState("");
    const [password, setPassword] = useState("");

    const handleSubmit = (e) => {
        e.preventDefault();
        console.log({ email, password });
    };

    return (
        <form onSubmit={handleSubmit}>
            <input
                type="email"
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                placeholder="Email"
            />
            <input
                type="password"
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                placeholder="Password"
            />
            <button type="submit">Login</button>
        </form>
    );
}
```

### Generic Form Handler
**Definition:** Handle multiple inputs with one onChange handler using input `name` attribute.
```jsx
function RegisterForm() {
    const [formData, setFormData] = useState({
        firstName: "", lastName: "", email: "", age: ""
    });

    // Generic handler — uses input name as key
    const handleChange = (e) => {
        const { name, value, type, checked } = e.target;
        setFormData(prev => ({
            ...prev,
            [name]: type === 'checkbox' ? checked : value
        }));
    };

    const handleSubmit = (e) => {
        e.preventDefault();
        console.log(formData);
    };

    return (
        <form onSubmit={handleSubmit}>
            <input name="firstName" value={formData.firstName} onChange={handleChange} />
            <input name="lastName"  value={formData.lastName}  onChange={handleChange} />
            <input name="email"     value={formData.email}     onChange={handleChange} type="email" />
            <button type="submit">Register</button>
        </form>
    );
}
```

### Select, Textarea, Checkbox
**Definition:** Controlled versions of other form elements.
```jsx
function FormElements() {
    const [selected, setSelected]   = useState("option1");
    const [text, setText]           = useState("");
    const [checked, setChecked]     = useState(false);
    const [agreed, setAgreed]       = useState([]);

    // Multi-checkbox
    const handleMultiCheck = (e) => {
        const { value, checked } = e.target;
        setAgreed(prev =>
            checked ? [...prev, value] : prev.filter(v => v !== value)
        );
    };

    return (
        <form>
            {/* Select dropdown */}
            <select value={selected} onChange={e => setSelected(e.target.value)}>
                <option value="option1">Option 1</option>
                <option value="option2">Option 2</option>
            </select>

            {/* Textarea */}
            <textarea value={text} onChange={e => setText(e.target.value)} rows={4} />

            {/* Single checkbox */}
            <input type="checkbox" checked={checked} onChange={e => setChecked(e.target.checked)} />

            {/* Multi checkboxes */}
            {["html", "css", "js"].map(skill => (
                <label key={skill}>
                    <input
                        type="checkbox"
                        value={skill}
                        checked={agreed.includes(skill)}
                        onChange={handleMultiCheck}
                    />
                    {skill}
                </label>
            ))}
        </form>
    );
}
```

---

## useEffect

**Definition:** Run side effects after render — data fetching, subscriptions, timers, and DOM manipulation.

### Basic useEffect
**Definition:** The effect runs after every render by default — add dependency array to control when it runs.
```jsx
import { useState, useEffect } from 'react';

function Component() {
    const [count, setCount] = useState(0);

    // Run after every render
    useEffect(() => {
        document.title = `Count: ${count}`;
    });

    // Run only once — on mount
    useEffect(() => {
        console.log("Component mounted");
    }, []);    // Empty array = run once

    // Run when count changes
    useEffect(() => {
        console.log("Count changed to:", count);
    }, [count]);

    // Run when multiple values change
    useEffect(() => {
        fetchData(userId, page);
    }, [userId, page]);

    return <button onClick={() => setCount(c => c + 1)}>{count}</button>;
}
```

### Cleanup Function
**Definition:** Return a function from useEffect to clean up subscriptions and timers — runs before next effect and on unmount.
```jsx
function Timer() {
    const [seconds, setSeconds] = useState(0);

    useEffect(() => {
        const interval = setInterval(() => {
            setSeconds(s => s + 1);
        }, 1000);

        // Cleanup — clear interval when component unmounts or re-runs
        return () => clearInterval(interval);
    }, []);    // Only start once

    return <p>Seconds: {seconds}</p>;
}

// Event listener cleanup
function WindowSize() {
    const [size, setSize] = useState({ w: window.innerWidth, h: window.innerHeight });

    useEffect(() => {
        const handleResize = () =>
            setSize({ w: window.innerWidth, h: window.innerHeight });

        window.addEventListener('resize', handleResize);
        return () => window.removeEventListener('resize', handleResize);
    }, []);

    return <p>{size.w} × {size.h}</p>;
}
```

### Fetch Data with useEffect
**Definition:** Fetch data on mount or when dependencies change — handle loading and error states.
```jsx
function UserProfile({ userId }) {
    const [user,    setUser]    = useState(null);
    const [loading, setLoading] = useState(true);
    const [error,   setError]   = useState(null);

    useEffect(() => {
        let cancelled = false;    // Prevent state update on unmounted component

        const fetchUser = async () => {
            setLoading(true);
            setError(null);
            try {
                const res  = await fetch(`/api/users/${userId}`);
                if (!res.ok) throw new Error(`HTTP ${res.status}`);
                const data = await res.json();
                if (!cancelled) setUser(data);
            } catch (err) {
                if (!cancelled) setError(err.message);
            } finally {
                if (!cancelled) setLoading(false);
            }
        };

        fetchUser();
        return () => { cancelled = true; };
    }, [userId]);

    if (loading) return <Spinner />;
    if (error)   return <ErrorMessage message={error} />;
    if (!user)   return null;
    return <UserCard user={user} />;
}
```

---

## useRef

**Definition:** Holds a mutable value that persists across renders without causing re-renders — access DOM elements or store previous values.

### DOM Reference
**Definition:** Get a direct reference to a DOM element for focus, measurements, or imperative actions.
```jsx
import { useRef } from 'react';

function FocusInput() {
    const inputRef = useRef(null);

    const focusInput = () => {
        inputRef.current.focus();
    };

    const clearInput = () => {
        inputRef.current.value = "";
        inputRef.current.focus();
    };

    return (
        <div>
            <input ref={inputRef} type="text" placeholder="Click button to focus" />
            <button onClick={focusInput}>Focus</button>
            <button onClick={clearInput}>Clear</button>
        </div>
    );
}
```

### Store Mutable Value
**Definition:** Store any mutable value that survives re-renders without triggering a re-render.
```jsx
function Stopwatch() {
    const [time, setTime]     = useState(0);
    const [running, setRunning] = useState(false);
    const intervalRef = useRef(null);    // Store interval ID without re-rendering

    const start = () => {
        setRunning(true);
        intervalRef.current = setInterval(() => setTime(t => t + 1), 1000);
    };

    const stop = () => {
        setRunning(false);
        clearInterval(intervalRef.current);
    };

    return (
        <div>
            <p>{time}s</p>
            <button onClick={running ? stop : start}>{running ? "Stop" : "Start"}</button>
        </div>
    );
}
```

### Previous Value
**Definition:** Track the previous value of a prop or state using useRef.
```jsx
function usePrevious(value) {
    const ref = useRef();

    useEffect(() => {
        ref.current = value;    // Update AFTER render
    }, [value]);

    return ref.current;    // Returns value from previous render
}

function Counter() {
    const [count, setCount] = useState(0);
    const prevCount = usePrevious(count);

    return (
        <p>
            Now: {count} | Before: {prevCount ?? "—"}
        </p>
    );
}
```

---

## useContext

**Definition:** Access shared data from a Context without prop drilling — any component in the tree can read context.

### Create and Use Context
**Definition:** Create a context, provide a value, and consume it anywhere in the component tree.
```jsx
import { createContext, useContext, useState } from 'react';

// 1. Create context with default value
const ThemeContext = createContext('light');

// 2. Provider wraps the tree that needs access
function App() {
    const [theme, setTheme] = useState('light');

    return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
            <Header />
            <Main />
            <Footer />
        </ThemeContext.Provider>
    );
}

// 3. Consume anywhere in the tree — no prop drilling!
function Header() {
    const { theme, setTheme } = useContext(ThemeContext);

    return (
        <header className={`header--${theme}`}>
            <button onClick={() => setTheme(t => t === 'light' ? 'dark' : 'light')}>
                Toggle Theme
            </button>
        </header>
    );
}
```

---

## useReducer

**Definition:** Manage complex state logic with a reducer function — like Redux but built into React.

### Basic useReducer
**Definition:** Define state transitions as actions in a reducer function — better than useState for complex state.
```jsx
import { useReducer } from 'react';

// Reducer — pure function: (state, action) => newState
function counterReducer(state, action) {
    switch (action.type) {
        case 'INCREMENT':
            return { count: state.count + 1 };
        case 'DECREMENT':
            return { count: state.count - 1 };
        case 'RESET':
            return { count: 0 };
        case 'SET':
            return { count: action.payload };
        default:
            throw new Error(`Unknown action: ${action.type}`);
    }
}

function Counter() {
    const [state, dispatch] = useReducer(counterReducer, { count: 0 });

    return (
        <div>
            <p>Count: {state.count}</p>
            <button onClick={() => dispatch({ type: 'INCREMENT' })}>+</button>
            <button onClick={() => dispatch({ type: 'DECREMENT' })}>-</button>
            <button onClick={() => dispatch({ type: 'RESET' })}>Reset</button>
            <button onClick={() => dispatch({ type: 'SET', payload: 10 })}>Set 10</button>
        </div>
    );
}
```

### useReducer for Complex State
**Definition:** Use useReducer when state has multiple related values or complex transition logic.
```jsx
const initialState = {
    users:   [],
    loading: false,
    error:   null,
    page:    1
};

function usersReducer(state, action) {
    switch (action.type) {
        case 'FETCH_START':
            return { ...state, loading: true, error: null };
        case 'FETCH_SUCCESS':
            return { ...state, loading: false, users: action.payload };
        case 'FETCH_ERROR':
            return { ...state, loading: false, error: action.payload };
        case 'NEXT_PAGE':
            return { ...state, page: state.page + 1 };
        case 'DELETE_USER':
            return {
                ...state,
                users: state.users.filter(u => u.id !== action.payload)
            };
        default:
            return state;
    }
}

function UsersList() {
    const [state, dispatch] = useReducer(usersReducer, initialState);

    useEffect(() => {
        dispatch({ type: 'FETCH_START' });
        fetchUsers(state.page)
            .then(data => dispatch({ type: 'FETCH_SUCCESS', payload: data }))
            .catch(err => dispatch({ type: 'FETCH_ERROR', payload: err.message }));
    }, [state.page]);

    if (state.loading) return <Spinner />;
    if (state.error)   return <Error message={state.error} />;
    return <UserList users={state.users} onDelete={id => dispatch({ type: 'DELETE_USER', payload: id })} />;
}
```

---

## useMemo

**Definition:** Memoize an expensive computed value — only recalculates when dependencies change.

### Basic useMemo
**Definition:** Cache the result of a heavy computation between renders.
```jsx
import { useMemo, useState } from 'react';

function DataTable({ items, filter, sortBy }) {
    // Expensive — only recompute when items, filter, or sortBy changes
    const processedItems = useMemo(() => {
        console.log("Computing...");   // Won't run on every re-render
        return items
            .filter(item => item.name.includes(filter))
            .sort((a, b) => a[sortBy] > b[sortBy] ? 1 : -1);
    }, [items, filter, sortBy]);

    return (
        <table>
            {processedItems.map(item => (
                <tr key={item.id}><td>{item.name}</td></tr>
            ))}
        </table>
    );
}

// Memoize a derived object to preserve reference
function ComponentA({ data }) {
    const config = useMemo(() => ({
        theme: data.theme,
        locale: data.locale
    }), [data.theme, data.locale]);

    return <ComponentB config={config} />;
}
```

---

## useCallback

**Definition:** Memoize a function reference — prevents child components from re-rendering when the function hasn't changed.

### Basic useCallback
**Definition:** Return the same function reference between renders — useful when passing callbacks to memoized children.
```jsx
import { useCallback, useState, memo } from 'react';

// Memoized child — only re-renders if props change
const ExpensiveChild = memo(function ExpensiveChild({ onSubmit, label }) {
    console.log("Child rendered");
    return <button onClick={onSubmit}>{label}</button>;
});

function Parent() {
    const [count, setCount] = useState(0);
    const [text,  setText]  = useState("");

    // WITHOUT useCallback — new function every render → child always re-renders
    const handleSubmit = () => console.log("Submitted");

    // WITH useCallback — same function reference → child only re-renders when needed
    const handleSubmit = useCallback(() => {
        console.log("Submitted:", text);
    }, [text]);    // Only new function when text changes

    return (
        <div>
            <input value={text} onChange={e => setText(e.target.value)} />
            <button onClick={() => setCount(c => c + 1)}>Count: {count}</button>

            {/* Won't re-render when count changes — only when text changes */}
            <ExpensiveChild onSubmit={handleSubmit} label="Submit" />
        </div>
    );
}
```

---

## Custom Hooks

**Definition:** Extract reusable stateful logic into functions starting with `use` — share logic without sharing UI.

### Simple Custom Hook
**Definition:** A function that uses React hooks and can be reused across multiple components.
```jsx
// useCounter hook
function useCounter(initialValue = 0, step = 1) {
    const [count, setCount] = useState(initialValue);

    const increment = useCallback(() => setCount(c => c + step), [step]);
    const decrement = useCallback(() => setCount(c => c - step), [step]);
    const reset     = useCallback(() => setCount(initialValue), [initialValue]);

    return { count, increment, decrement, reset };
}

// Use in any component
function App() {
    const { count, increment, decrement, reset } = useCounter(0, 2);
    return (
        <div>
            <p>{count}</p>
            <button onClick={increment}>+2</button>
            <button onClick={decrement}>-2</button>
            <button onClick={reset}>Reset</button>
        </div>
    );
}
```

### useFetch Hook
**Definition:** Reusable data fetching logic — handles loading, error, and abort.
```jsx
function useFetch(url) {
    const [data,    setData]    = useState(null);
    const [loading, setLoading] = useState(true);
    const [error,   setError]   = useState(null);

    useEffect(() => {
        const controller = new AbortController();

        const fetchData = async () => {
            setLoading(true);
            setError(null);
            try {
                const res  = await fetch(url, { signal: controller.signal });
                if (!res.ok) throw new Error(`HTTP ${res.status}`);
                const json = await res.json();
                setData(json);
            } catch (err) {
                if (err.name !== 'AbortError') setError(err.message);
            } finally {
                setLoading(false);
            }
        };

        fetchData();
        return () => controller.abort();
    }, [url]);

    return { data, loading, error };
}

// Usage
function UserProfile({ id }) {
    const { data: user, loading, error } = useFetch(`/api/users/${id}`);

    if (loading) return <Spinner />;
    if (error)   return <Error message={error} />;
    return <UserCard user={user} />;
}
```

### useLocalStorage Hook
**Definition:** Sync state with localStorage — persists across page reloads.
```jsx
function useLocalStorage(key, initialValue) {
    const [value, setValue] = useState(() => {
        try {
            const item = localStorage.getItem(key);
            return item ? JSON.parse(item) : initialValue;
        } catch {
            return initialValue;
        }
    });

    const setStoredValue = useCallback((val) => {
        setValue(val);
        localStorage.setItem(key, JSON.stringify(
            val instanceof Function ? val(value) : val
        ));
    }, [key, value]);

    return [value, setStoredValue];
}

// Usage
function Settings() {
    const [theme, setTheme] = useLocalStorage('theme', 'light');
    return (
        <button onClick={() => setTheme(t => t === 'light' ? 'dark' : 'light')}>
            Theme: {theme}
        </button>
    );
}
```

---

## Component Lifecycle (with Hooks)

**Definition:** Understand how hooks map to the traditional class component lifecycle phases.

### Lifecycle Phases
**Definition:** The three phases of a React component's life mapped to hooks.
```jsx
function LifecycleDemo({ userId }) {
    const [data, setData] = useState(null);

    // ── MOUNT (componentDidMount) ─────────────────────
    useEffect(() => {
        console.log("Component mounted");
        subscribeToUpdates();
        // ...
    }, []);    // Empty deps = runs once on mount

    // ── UPDATE (componentDidUpdate) ──────────────────
    useEffect(() => {
        console.log("userId changed, fetching new data");
        fetchData(userId).then(setData);
    }, [userId]);    // Runs when userId changes

    // ── UNMOUNT (componentWillUnmount) ───────────────
    useEffect(() => {
        return () => {
            console.log("Component will unmount");
            unsubscribeFromUpdates();    // Cleanup
        };
    }, []);    // Empty deps = cleanup only on unmount

    // ── BOTH mount and update ─────────────────────────
    useEffect(() => {
        console.log("Ran after every render");
    });    // No deps array

    return <div>{data?.name}</div>;
}
```

---

## Fragments

**Definition:** Group multiple elements without adding an extra DOM node — React requires a single root element.

### Fragment Syntax
**Definition:** Two syntaxes — long form accepts a `key` prop, short form is cleaner.
```jsx
import { Fragment } from 'react';

// Long form — supports key prop (useful in lists)
function ListItems({ items }) {
    return items.map(item => (
        <Fragment key={item.id}>
            <dt>{item.term}</dt>
            <dd>{item.definition}</dd>
        </Fragment>
    ));
}

// Short form — cleaner, most common
function UserFields() {
    return (
        <>
            <input name="firstName" placeholder="First Name" />
            <input name="lastName"  placeholder="Last Name" />
            <input name="email"     placeholder="Email" />
        </>
    );
}
```

---

## Portals

**Definition:** Render a child component outside its parent DOM hierarchy — useful for modals and tooltips.

### Create a Portal
**Definition:** `ReactDOM.createPortal` renders into a different DOM node while preserving React context.
```jsx
import ReactDOM from 'react-dom';

function Modal({ isOpen, onClose, children }) {
    if (!isOpen) return null;

    // Renders into document.body, not the parent component's DOM
    return ReactDOM.createPortal(
        <div className="modal-overlay" onClick={onClose}>
            <div className="modal-content" onClick={e => e.stopPropagation()}>
                <button className="modal-close" onClick={onClose}>×</button>
                {children}
            </div>
        </div>,
        document.body    // Target DOM node
    );
}

// Usage
function App() {
    const [isOpen, setIsOpen] = useState(false);

    return (
        <div>
            <button onClick={() => setIsOpen(true)}>Open Modal</button>
            <Modal isOpen={isOpen} onClose={() => setIsOpen(false)}>
                <h2>Modal Title</h2>
                <p>Modal content here.</p>
            </Modal>
        </div>
    );
}
```

---

## Error Boundaries

**Definition:** Catch JavaScript errors in child components — display fallback UI instead of crashing.

### Create Error Boundary
**Definition:** Error boundaries must be class components — wrap any component tree to catch errors.
```jsx
import { Component } from 'react';

class ErrorBoundary extends Component {
    constructor(props) {
        super(props);
        this.state = { hasError: false, error: null };
    }

    // Called when a descendant throws
    static getDerivedStateFromError(error) {
        return { hasError: true, error };
    }

    // For logging errors to error tracking service
    componentDidCatch(error, errorInfo) {
        console.error('Error caught:', error, errorInfo);
        logErrorToService(error, errorInfo);
    }

    render() {
        if (this.state.hasError) {
            return this.props.fallback || (
                <div className="error-ui">
                    <h2>Something went wrong.</h2>
                    <button onClick={() => this.setState({ hasError: false })}>
                        Try Again
                    </button>
                </div>
            );
        }
        return this.props.children;
    }
}

// Usage
function App() {
    return (
        <ErrorBoundary fallback={<p>Failed to load this section.</p>}>
            <UserDashboard />
        </ErrorBoundary>
    );
}
```

---

## Lazy Loading & Suspense

**Definition:** Load components on demand to split bundles — improve initial load performance.

### React.lazy & Suspense
**Definition:** Dynamically import a component — `Suspense` shows a fallback while it loads.
```jsx
import { lazy, Suspense } from 'react';

// Lazy load — only downloaded when needed
const Dashboard   = lazy(() => import('./Dashboard'));
const Settings    = lazy(() => import('./Settings'));
const AdminPanel  = lazy(() => import('./AdminPanel'));

function App() {
    const [page, setPage] = useState('dashboard');

    return (
        <div>
            <nav>
                <button onClick={() => setPage('dashboard')}>Dashboard</button>
                <button onClick={() => setPage('settings')}>Settings</button>
            </nav>

            {/* Suspense shows fallback while lazy component loads */}
            <Suspense fallback={<div>Loading...</div>}>
                {page === 'dashboard' && <Dashboard />}
                {page === 'settings'  && <Settings />}
            </Suspense>
        </div>
    );
}

// Named lazy imports (default export required by React.lazy)
const Component = lazy(() =>
    import('./module').then(module => ({ default: module.NamedExport }))
);
```

---

## Higher-Order Components

**Definition:** A function that takes a component and returns a new enhanced component — a reusable logic pattern.

### HOC Pattern
**Definition:** Wrap a component to add behavior — common for logging, authentication, and data fetching.
```jsx
// HOC that adds loading state
function withLoading(WrappedComponent) {
    return function WithLoading({ isLoading, ...props }) {
        if (isLoading) return <Spinner />;
        return <WrappedComponent {...props} />;
    };
}

// HOC that requires authentication
function withAuth(WrappedComponent) {
    return function WithAuth(props) {
        const { isAuthenticated } = useAuth();

        if (!isAuthenticated) {
            return <Navigate to="/login" replace />;
        }

        return <WrappedComponent {...props} />;
    };
}

// Apply HOCs
const UserListWithLoading = withLoading(UserList);
const ProtectedDashboard  = withAuth(Dashboard);

// Usage
<UserListWithLoading isLoading={loading} users={users} />
<ProtectedDashboard />
```

---

## Render Props

**Definition:** Pass a function as a prop that returns JSX — share stateful logic between components.

### Render Prop Pattern
**Definition:** Component calls a function prop to render UI — the function receives shared state.
```jsx
// Component with shared logic exposes state via render prop
function MouseTracker({ render }) {
    const [position, setPosition] = useState({ x: 0, y: 0 });

    const handleMouseMove = (e) => {
        setPosition({ x: e.clientX, y: e.clientY });
    };

    return (
        <div onMouseMove={handleMouseMove} style={{ height: '300px' }}>
            {render(position)}
        </div>
    );
}

// Usage — you control what to render
<MouseTracker render={({ x, y }) => (
    <p>Mouse is at: {x}, {y}</p>
)} />

// "children as function" variant
function MouseTracker({ children }) {
    const [pos, setPos] = useState({ x: 0, y: 0 });
    return <div onMouseMove={e => setPos({ x: e.clientX, y: e.clientY })}>
        {children(pos)}
    </div>;
}

<MouseTracker>
    {({ x, y }) => <p>{x}, {y}</p>}
</MouseTracker>
```

---

## Compound Components

**Definition:** Multiple components that work together as a group — share implicit state through context.

### Compound Component Pattern
**Definition:** Parent manages state, children access it via context — flexible, composable API.
```jsx
const TabsContext = createContext(null);

function Tabs({ children, defaultTab }) {
    const [activeTab, setActiveTab] = useState(defaultTab);
    return (
        <TabsContext.Provider value={{ activeTab, setActiveTab }}>
            <div className="tabs">{children}</div>
        </TabsContext.Provider>
    );
}

function TabList({ children }) {
    return <div className="tab-list" role="tablist">{children}</div>;
}

function Tab({ id, children }) {
    const { activeTab, setActiveTab } = useContext(TabsContext);
    return (
        <button
            role="tab"
            aria-selected={activeTab === id}
            onClick={() => setActiveTab(id)}
            className={activeTab === id ? 'tab--active' : 'tab'}
        >
            {children}
        </button>
    );
}

function TabPanel({ id, children }) {
    const { activeTab } = useContext(TabsContext);
    if (activeTab !== id) return null;
    return <div role="tabpanel">{children}</div>;
}

// Attach as sub-components
Tabs.TabList  = TabList;
Tabs.Tab      = Tab;
Tabs.TabPanel = TabPanel;

// Clean, composable usage
function App() {
    return (
        <Tabs defaultTab="profile">
            <Tabs.TabList>
                <Tabs.Tab id="profile">Profile</Tabs.Tab>
                <Tabs.Tab id="settings">Settings</Tabs.Tab>
            </Tabs.TabList>
            <Tabs.TabPanel id="profile"><ProfileContent /></Tabs.TabPanel>
            <Tabs.TabPanel id="settings"><SettingsContent /></Tabs.TabPanel>
        </Tabs>
    );
}
```

---

## Forwarding Refs

**Definition:** Pass a ref through a component to a DOM element inside it — needed for libraries and focus management.

### forwardRef
**Definition:** Wrap a component with `forwardRef` to allow parents to access its inner DOM element.
```jsx
import { forwardRef } from 'react';

// Input that forwards ref to the underlying <input>
const FancyInput = forwardRef(function FancyInput({ label, ...props }, ref) {
    return (
        <div className="input-wrapper">
            <label>{label}</label>
            <input ref={ref} {...props} className="fancy-input" />
        </div>
    );
});

// Parent can directly access the DOM input
function LoginForm() {
    const emailRef = useRef(null);

    const handleSubmit = () => {
        emailRef.current.focus();    // Focus the inner input directly
    };

    return (
        <form>
            <FancyInput ref={emailRef} label="Email" type="email" />
            <button type="submit" onClick={handleSubmit}>Submit</button>
        </form>
    );
}
```

---

## Context API (Full Pattern)

**Definition:** A complete pattern for managing shared state with Context — create, provide, and consume.

### Full Context Pattern
**Definition:** Combine context with custom hooks for a clean, type-safe global state pattern.
```jsx
import { createContext, useContext, useReducer, useMemo } from 'react';

// 1. Define initial state and reducer
const initialState = { user: null, theme: 'light', notifications: [] };

function appReducer(state, action) {
    switch (action.type) {
        case 'SET_USER':        return { ...state, user: action.payload };
        case 'TOGGLE_THEME':    return { ...state, theme: state.theme === 'light' ? 'dark' : 'light' };
        case 'ADD_NOTIFICATION': return { ...state, notifications: [...state.notifications, action.payload] };
        case 'CLEAR_NOTIFICATIONS': return { ...state, notifications: [] };
        default: return state;
    }
}

// 2. Create context
const AppContext = createContext(null);

// 3. Create provider component
export function AppProvider({ children }) {
    const [state, dispatch] = useReducer(appReducer, initialState);

    // Memoize value to prevent unnecessary re-renders
    const value = useMemo(() => ({ state, dispatch }), [state]);

    return (
        <AppContext.Provider value={value}>
            {children}
        </AppContext.Provider>
    );
}

// 4. Custom hook — better DX than using useContext directly
export function useApp() {
    const context = useContext(AppContext);
    if (!context) throw new Error('useApp must be used within AppProvider');
    return context;
}

// 5. Usage anywhere in the tree
function Navbar() {
    const { state, dispatch } = useApp();

    return (
        <nav>
            <span>Welcome, {state.user?.name ?? 'Guest'}</span>
            <button onClick={() => dispatch({ type: 'TOGGLE_THEME' })}>
                Theme: {state.theme}
            </button>
        </nav>
    );
}

// 6. Wrap app
function App() {
    return (
        <AppProvider>
            <Navbar />
            <Main />
        </AppProvider>
    );
}
```

---

## Performance Optimization

**Definition:** Techniques to prevent unnecessary renders and keep React apps fast.

### When to Optimize
**Definition:** Profile first — don't optimize prematurely. React is fast by default.
```jsx
// React DevTools Profiler shows render time and counts
// Only optimize when you measure a real problem

// Common causes of unnecessary re-renders:
// 1. New object/array created on every render
// 2. Function recreated on every render
// 3. Context value changes too often
// 4. State too high in the component tree
```

### Optimization Checklist
**Definition:** Step-by-step guide to improving React performance.
```jsx
// 1. Move state down — keep state close to where it's used
// 2. Use React.memo for expensive pure components
// 3. Use useMemo for expensive calculations
// 4. Use useCallback for functions passed as props
// 5. Use lazy loading for large components
// 6. Virtualize long lists (react-window, react-virtual)
// 7. Avoid anonymous objects in JSX props

// BAD — new object created on every render
<Component style={{ color: 'red' }} />

// GOOD — defined outside or memoized
const style = { color: 'red' };    // Outside component
<Component style={style} />

// 8. Split context — separate frequently-changing from rarely-changing
const UserContext    = createContext(null);    // Changes rarely
const ThemeContext   = createContext(null);    // Changes often
```

---

## React.memo

**Definition:** Memoize a component — skip re-rendering if props haven't changed.

### Basic React.memo
**Definition:** Wrap a component with `memo` — it only re-renders when its props change.
```jsx
import { memo } from 'react';

// Expensive component — only re-renders when user changes
const UserCard = memo(function UserCard({ user, onDelete }) {
    console.log("UserCard rendered for", user.name);
    return (
        <div className="card">
            <h3>{user.name}</h3>
            <button onClick={() => onDelete(user.id)}>Delete</button>
        </div>
    );
});

// Custom comparison function
const UserCard = memo(function UserCard({ user }) {
    return <div>{user.name}</div>;
}, (prevProps, nextProps) => {
    // Return true to SKIP re-render (props are equal)
    return prevProps.user.id === nextProps.user.id &&
           prevProps.user.name === nextProps.user.name;
});

// Combine with useCallback for stable function references
function UserList({ users }) {
    const handleDelete = useCallback((id) => {
        deleteUser(id);
    }, []);    // Stable reference — UserCard won't re-render

    return users.map(user => (
        <UserCard key={user.id} user={user} onDelete={handleDelete} />
    ));
}
```

---

## Styling in React

**Definition:** Multiple approaches for styling React components — choose based on project scale and preferences.

### CSS Modules
**Definition:** Locally-scoped CSS — class names are unique, no global conflicts.
```jsx
// Button.module.css
.button { padding: 8px 16px; border-radius: 4px; }
.primary { background: blue; color: white; }
.danger  { background: red;  color: white; }

// Button.jsx
import styles from './Button.module.css';

function Button({ variant = 'primary', children }) {
    return (
        <button className={`${styles.button} ${styles[variant]}`}>
            {children}
        </button>
    );
}
```

### Inline Styles
**Definition:** Style objects passed directly — useful for dynamic values.
```jsx
function DynamicBox({ color, size }) {
    const style = {
        backgroundColor: color,
        width:  `${size}px`,
        height: `${size}px`,
        borderRadius: '50%'
    };

    return <div style={style} />;
}
```

### clsx / classnames
**Definition:** Build className strings conditionally — widely used utility.
```jsx
import clsx from 'clsx';

function Button({ variant, size, disabled, className }) {
    return (
        <button
            className={clsx(
                'btn',
                `btn-${variant}`,
                size && `btn-${size}`,
                disabled && 'btn-disabled',
                className
            )}
            disabled={disabled}
        >
            Click Me
        </button>
    );
}
```

### Tailwind CSS
**Definition:** Utility classes applied directly in JSX — popular with React.
```jsx
function Card({ title, children }) {
    return (
        <div className="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow">
            <h2 className="text-xl font-bold text-gray-800 mb-4">{title}</h2>
            <div className="text-gray-600">{children}</div>
        </div>
    );
}
```

---

## React Router (v6)

**Definition:** Client-side routing for React — navigate between pages without full page reloads.

### Setup & Basic Routing
**Definition:** Wrap your app in `BrowserRouter` and define routes with `Routes` and `Route`.
```jsx
import { BrowserRouter, Routes, Route, Link, NavLink, Navigate } from 'react-router-dom';

function App() {
    return (
        <BrowserRouter>
            <nav>
                <NavLink to="/"        className={({ isActive }) => isActive ? 'active' : ''}>Home</NavLink>
                <NavLink to="/about"   className={({ isActive }) => isActive ? 'active' : ''}>About</NavLink>
                <NavLink to="/users"   className={({ isActive }) => isActive ? 'active' : ''}>Users</NavLink>
            </nav>

            <Routes>
                <Route path="/"          element={<Home />} />
                <Route path="/about"     element={<About />} />
                <Route path="/users"     element={<Users />} />
                <Route path="/users/:id" element={<UserDetail />} />
                <Route path="*"          element={<NotFound />} />    {/* 404 */}
                <Route path="/old"       element={<Navigate to="/new" replace />} />
            </Routes>
        </BrowserRouter>
    );
}
```

### Hooks
**Definition:** React Router provides hooks for navigation, params, and URL data.
```jsx
import {
    useNavigate, useParams, useLocation,
    useSearchParams, useMatch
} from 'react-router-dom';

function UserDetail() {
    const { id }      = useParams();        // /users/:id → { id: "42" }
    const navigate    = useNavigate();
    const location    = useLocation();      // Current URL info
    const [searchParams, setSearchParams] = useSearchParams();
    // /search?q=dark&page=2 → searchParams.get('q') = "dark"

    const goBack  = () => navigate(-1);
    const goHome  = () => navigate('/');
    const goUser  = () => navigate(`/users/${id}/edit`, { state: { from: 'detail' } });

    return (
        <div>
            <p>User ID: {id}</p>
            <p>Path: {location.pathname}</p>
            <p>Search: {searchParams.get('q')}</p>
            <button onClick={goBack}>Back</button>
            <button onClick={goHome}>Home</button>
        </div>
    );
}
```

### Protected Routes
**Definition:** Redirect unauthenticated users to login using a wrapper component.
```jsx
function PrivateRoute({ children }) {
    const { isAuthenticated } = useAuth();
    const location = useLocation();

    if (!isAuthenticated) {
        // Save current path to redirect back after login
        return <Navigate to="/login" state={{ from: location }} replace />;
    }

    return children;
}

// Nested layout routes
<Routes>
    <Route path="/"         element={<Layout />}>
        <Route index         element={<Home />} />
        <Route path="about"  element={<About />} />
        <Route path="app"    element={<PrivateRoute><AppLayout /></PrivateRoute>}>
            <Route index     element={<Dashboard />} />
            <Route path="settings" element={<Settings />} />
        </Route>
    </Route>
</Routes>
```

---

## Data Fetching Patterns

**Definition:** Common approaches for fetching and caching server data in React applications.

### useEffect Pattern
**Definition:** The basic pattern — fetch in useEffect, handle loading and error states.
```jsx
function useData(url) {
    const [state, setState] = useState({ data: null, loading: true, error: null });

    useEffect(() => {
        const controller = new AbortController();
        setState(prev => ({ ...prev, loading: true }));

        fetch(url, { signal: controller.signal })
            .then(r => r.ok ? r.json() : Promise.reject(r.statusText))
            .then(data => setState({ data, loading: false, error: null }))
            .catch(err => {
                if (err.name !== 'AbortError')
                    setState({ data: null, loading: false, error: err });
            });

        return () => controller.abort();
    }, [url]);

    return state;
}
```

### React Query (TanStack Query)
**Definition:** Server state management library — handles caching, refetching, and synchronization automatically.
```jsx
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

// Fetch with automatic caching and refetching
function UserProfile({ userId }) {
    const { data: user, isLoading, isError, error } = useQuery({
        queryKey: ['user', userId],
        queryFn:  () => fetch(`/api/users/${userId}`).then(r => r.json()),
        staleTime: 5 * 60 * 1000,    // Cache for 5 minutes
    });

    if (isLoading) return <Spinner />;
    if (isError)   return <Error message={error.message} />;
    return <UserCard user={user} />;
}

// Mutation with cache invalidation
function DeleteButton({ userId }) {
    const queryClient = useQueryClient();

    const deleteMutation = useMutation({
        mutationFn: (id) => fetch(`/api/users/${id}`, { method: 'DELETE' }),
        onSuccess:  () => queryClient.invalidateQueries({ queryKey: ['users'] }),
    });

    return (
        <button
            onClick={() => deleteMutation.mutate(userId)}
            disabled={deleteMutation.isPending}
        >
            {deleteMutation.isPending ? 'Deleting...' : 'Delete'}
        </button>
    );
}
```

---

## TypeScript with React

**Definition:** Type-safe React — catch bugs at compile time with TypeScript.

### Component Types
**Definition:** Type props, state, and event handlers for full type safety.
```tsx
import { FC, ReactNode, ChangeEvent, MouseEvent } from 'react';

// Type props with interface
interface ButtonProps {
    label:     string;
    onClick:   () => void;
    variant?:  'primary' | 'secondary' | 'danger';
    disabled?: boolean;
    children?: ReactNode;
}

// Functional component with typed props
const Button: FC<ButtonProps> = ({ label, onClick, variant = 'primary', disabled = false }) => {
    return (
        <button
            className={`btn btn-${variant}`}
            onClick={onClick}
            disabled={disabled}
        >
            {label}
        </button>
    );
};

// Inline typed props
function Input({ value, onChange }: { value: string; onChange: (val: string) => void }) {
    return <input value={value} onChange={e => onChange(e.target.value)} />;
}
```

### Hooks with TypeScript
**Definition:** Type useState, useRef, useReducer, and useContext properly.
```tsx
// useState — type inferred
const [count, setCount] = useState(0);           // number
const [user,  setUser]  = useState<User | null>(null);   // explicit generic

// useRef — DOM element
const inputRef = useRef<HTMLInputElement>(null);
const divRef   = useRef<HTMLDivElement>(null);

// useRef — mutable value
const intervalRef = useRef<ReturnType<typeof setInterval> | null>(null);

// useReducer — typed state and actions
interface State { count: number; error: string | null; }
type Action =
    | { type: 'INCREMENT' }
    | { type: 'SET_ERROR'; payload: string };

const [state, dispatch] = useReducer<React.Reducer<State, Action>>(
    reducer, { count: 0, error: null }
);

// useContext — non-null assertion
const context = useContext(ThemeContext);
if (!context) throw new Error('Must be inside ThemeProvider');

// Event handlers
const handleChange = (e: ChangeEvent<HTMLInputElement>) => {};
const handleClick  = (e: MouseEvent<HTMLButtonElement>) => {};
const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {};
```

---

## Testing React Components

**Definition:** Test React components with React Testing Library — test behavior, not implementation.

### Basic Tests
**Definition:** Render components and assert on their output and behavior.
```jsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { Counter } from './Counter';

describe('Counter', () => {
    test('renders initial count', () => {
        render(<Counter initialCount={5} />);
        expect(screen.getByText('Count: 5')).toBeInTheDocument();
    });

    test('increments when + button clicked', async () => {
        const user = userEvent.setup();
        render(<Counter />);

        await user.click(screen.getByRole('button', { name: /increment/i }));
        expect(screen.getByText('Count: 1')).toBeInTheDocument();
    });

    test('calls onCountChange when count changes', async () => {
        const mockFn = jest.fn();
        const user   = userEvent.setup();
        render(<Counter onCountChange={mockFn} />);

        await user.click(screen.getByRole('button', { name: /increment/i }));
        expect(mockFn).toHaveBeenCalledWith(1);
    });
});
```

### Testing Async Components
**Definition:** Test components that fetch data or have async behavior.
```jsx
import { render, screen, waitFor } from '@testing-library/react';
import { rest } from 'msw';
import { setupServer } from 'msw/node';

// Mock API server
const server = setupServer(
    rest.get('/api/users/1', (req, res, ctx) => {
        return res(ctx.json({ id: 1, name: 'Dark', email: 'dark@example.com' }));
    })
);

beforeAll(()  => server.listen());
afterEach(()  => server.resetHandlers());
afterAll(()   => server.close());

test('displays user data', async () => {
    render(<UserProfile userId={1} />);

    // Loading state
    expect(screen.getByText(/loading/i)).toBeInTheDocument();

    // Wait for data
    await waitFor(() => {
        expect(screen.getByText('Dark')).toBeInTheDocument();
        expect(screen.getByText('dark@example.com')).toBeInTheDocument();
    });
});
```

---

## Project Setup

**Definition:** Set up a React project with modern tooling.

### Create React App / Vite
**Definition:** Two popular ways to scaffold a new React project.
```bash
# Vite — modern, fast (recommended)
npm create vite@latest my-app -- --template react
npm create vite@latest my-app -- --template react-ts   # with TypeScript

# Create React App (older, heavier)
npx create-react-app my-app
npx create-react-app my-app --template typescript

# Install and run
cd my-app
npm install
npm run dev     # Vite
npm start       # CRA
```

### Project Structure
**Definition:** Common folder structure for React applications.
```
src/
├── components/          ← Reusable UI components
│   ├── Button/
│   │   ├── Button.jsx
│   │   ├── Button.module.css
│   │   └── Button.test.jsx
│   └── Modal/
├── pages/               ← Page-level components (routes)
│   ├── Home.jsx
│   └── Dashboard.jsx
├── hooks/               ← Custom hooks
│   ├── useFetch.js
│   └── useLocalStorage.js
├── context/             ← Context providers
│   └── AppContext.jsx
├── services/            ← API calls, external services
│   └── api.js
├── utils/               ← Helper functions
│   └── formatDate.js
├── assets/              ← Images, fonts, icons
├── styles/              ← Global CSS, variables
│   └── globals.css
├── App.jsx
└── main.jsx
```

### Essential Packages
**Definition:** Commonly installed packages for most React projects.
```bash
# Routing
npm install react-router-dom

# State management
npm install @reduxjs/toolkit react-redux   # Redux
npm install zustand                         # Lightweight alternative

# Data fetching
npm install @tanstack/react-query

# Forms
npm install react-hook-form zod

# Styling
npm install tailwindcss postcss autoprefixer
npm install clsx

# Testing
npm install -D @testing-library/react @testing-library/user-event vitest jsdom

# TypeScript
npm install -D typescript @types/react @types/react-dom
```

---

## Tips & Tricks

**Definition:** Useful React patterns and shortcuts that save time and prevent bugs.

### Useful Patterns
**Definition:** Practical patterns for common React situations.
```jsx
// 1. Default export + named export
export default function Home() { }
export { Home };

// 2. Component with display name (useful in DevTools)
const MyComponent = React.memo(function MyComponent() { });

// 3. Optional chaining everywhere
user?.profile?.avatar?.url ?? '/default-avatar.png'

// 4. Key as reset mechanism — new key = fresh mount
<UserForm key={userId} userId={userId} />

// 5. Initializer pattern — avoid stale closures
const [items, setItems] = useState([]);
setItems(prev => [...prev, newItem]);    // Always use prev

// 6. useSyncExternalStore for external state
const snapshot = useSyncExternalStore(store.subscribe, store.getSnapshot);

// 7. useId for accessible labels (React 18+)
const id = useId();
<label htmlFor={id}>Name</label>
<input id={id} />

// 8. startTransition for non-urgent updates (React 18+)
import { startTransition } from 'react';
startTransition(() => setSearchQuery(input));

// 9. Controlled component from uncontrolled
const [value, setValue] = useState(initialValue ?? '');

// 10. Render nothing idiom
if (!data) return null;
```

### Common Mistakes to Avoid
**Definition:** Frequent React bugs and how to prevent them.
```jsx
// ❌ Don't call hooks conditionally
if (condition) {
    const [state, setState] = useState(0);   // WRONG
}

// ❌ Don't mutate state directly
state.push(item);             // WRONG
setState([...state, item]);   // CORRECT

// ❌ Missing key or using index as key for dynamic lists
items.map((item, i) => <Item key={i} />)  // BAD when items reorder

// ❌ useEffect with missing dependency
useEffect(() => {
    doSomethingWith(userId);
}, []);  // WRONG — userId missing from deps

// ❌ Infinite useEffect loop
useEffect(() => {
    setCount(count + 1);   // State update in effect with that state in deps
}, [count]);               // Infinite loop!

// ✅ Use updater function instead
useEffect(() => {
    setCount(prev => prev + 1);
}, []);   // Only run once

// ❌ Creating objects/arrays in JSX — new reference every render
<Child style={{ margin: 0 }} items={[]} />   // New objects every render
```

---

## Best Practices

**Definition:** Guidelines for writing maintainable, performant, and professional React code.

### Component Design
**Definition:** Design components to be small, focused, and reusable.
```jsx
// 1. Single Responsibility — one component, one job
// BAD — UserCard does too much
function UserCard({ userId }) {
    // fetches data, formats it, displays it, handles deletion...
}

// GOOD — split concerns
function UserCard({ user, onDelete }) { }     // Presentational
function UserCardContainer({ userId }) { }    // Data fetching

// 2. Lifting state up — share state via common ancestor
// 3. Composition over configuration — prefer children prop
// 4. Keep components pure — same props = same output
// 5. Name components with PascalCase
// 6. Name event handlers with handle prefix
const handleClick  = () => { };
const handleSubmit = () => { };
```

### Hooks Rules
**Definition:** The two rules React enforces for using hooks.
```jsx
// Rule 1: Only call hooks at the top level
// NEVER in loops, conditionals, or nested functions
function Component() {
    // ✅ Always at the top level
    const [count, setCount] = useState(0);
    useEffect(() => { }, []);

    // ❌ Never in a condition
    if (someCondition) {
        const [x, setX] = useState(0);    // WRONG
    }
}

// Rule 2: Only call hooks from React functions
// ✅ Functional components
// ✅ Custom hooks (start with 'use')
// ❌ Regular JavaScript functions
```

### Code Organization
**Definition:** Consistent file and code organization patterns.
```jsx
// Recommended import order
import React, { useState, useEffect, useCallback } from 'react';  // React
import { Link, useNavigate } from 'react-router-dom';              // Libraries
import { UserCard, Button } from '../components';                  // Internal components
import { useAuth } from '../hooks/useAuth';                        // Custom hooks
import { formatDate } from '../utils';                             // Utilities
import styles from './Page.module.css';                            // Styles
import type { User } from '../types';                              // Types

// Component structure order
function MyComponent({ prop1, prop2 }) {
    // 1. Hooks
    const [state, setState] = useState();
    const navigate          = useNavigate();
    const { data }          = useFetch('/api/data');

    // 2. Derived state
    const filteredData = useMemo(() => data?.filter(/* ... */), [data]);

    // 3. Event handlers
    const handleSubmit = useCallback(() => { }, []);

    // 4. Effects
    useEffect(() => { }, []);

    // 5. Early returns
    if (!data) return null;

    // 6. Render
    return <div>{ }</div>;
}
```

### Summary of Rules

* Use **functional components** — never class components for new code
* Follow the **Rules of Hooks** — top level only, React functions only
* Name **custom hooks** starting with `use`
* Use **`key` with stable unique IDs** — never array index for dynamic lists
* Always use **functional setState** when new state depends on old state
* **Clean up** in useEffect — clear intervals, abort fetches, unsubscribe
* Use **React.memo + useCallback** together — memo without useCallback often doesn't help
* Prefer **composition** — small components and children prop over complex props
* **Don't fetch in useEffect** for production — use React Query or SWR
* **Profile before optimizing** — use React DevTools, don't guess

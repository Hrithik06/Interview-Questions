# 1. Avoid unnecessary re-renders in Functional Component.
To avoid unnecessary re-renders in functional React components, the most effective tool is React.memo. The useEffect hook is not designed for controlling re-renders; it is used for handling side effects in response to state or prop changes, not for optimizing rendering itself.
Comparison: React.memo vs useEffect

|       Feature       |                                 React.memo                                 |                        useEffect                       |
|:-------------------:|:--------------------------------------------------------------------------:|:------------------------------------------------------:|
| Purpose             | Memoizes functional components to prevent re-render if props are unchanged | Handles side effects after render                      |
| Prevents Re-render? | Yes, if props have not changed (shallow comparison)                        | No, does not affect rendering directly                 |
| Usage               | Wraps a component: React.memo(MyComponent)                                 | Runs code after render: useEffect(() => {...}, [deps]) |
| Typical Use Case    | Optimizing pure functional components                                      | Fetching data, subscriptions, DOM updates              |
### Best Practices

- Use React.memo: Wrap your functional component with React.memo to prevent it from re-rendering unless its props change. This is the primary tool for avoiding unnecessary renders in functional components

- Optimize Props: Ensure that props passed to memoized components are stable (avoid creating new objects or functions inline unless necessary), as React.memo uses shallow comparison

- useMemo & useCallback: Use useMemo to memoize expensive calculations and useCallback to memoize functions, preventing unnecessary re-renders of child components that depend on those values or callbacks

- useRef: Store mutable values that do not affect rendering with useRef to avoid triggering re-renders when those values change

# 2. Which prop types is used to pass a function?
To pass a function as a prop in a functional React component, you use the prop type func. This allows the parent component to provide a function to the child, which the child can then call as needed.

This pattern is commonly referred to as passing a callback function. In React, a "callback prop" means a function prop that the child component can invoke to notify the parent about an event or to trigger some action in the parent component. For example, you might pass an onClick or onSubmit function from a parent to a child component as a callback.

Example:

```js
function ParentComponent() {
  const handleClick = () => {
    alert("Button clicked!");
  };

  return <ChildComponent onButtonClick={handleClick} />;
}

function ChildComponent({ onButtonClick }) {
  return <button onClick={onButtonClick}>Click Me</button>;
}
```

PropTypes usage:

```js
import PropTypes from 'prop-types';

ChildComponent.propTypes = {
  onButtonClick: PropTypes.func.isRequired, // 'func' is the type for function props
};
```

So, to summarize:

- The prop type for a function is func when using PropTypes
- Passing a function as a prop is commonly called a callback function in React.

# 3. How Context differs from Redux?

React's Context API and Redux are both used for state management, but they differ significantly in architecture, complexity, and best use cases.

### **Core Differences**

| Aspect                | Context API                               | Redux                                      |
|-----------------------|-------------------------------------------|--------------------------------------------|
| **State Management**  | Decentralized (via Providers/Consumers)   | Centralized (single global store)          |
| **Setup**             | Minimal, built into React                 | Requires setup: store, actions, reducers   |
| **Best For**          | Small to medium apps, simple state        | Large, complex apps, advanced state needs  |
| **Performance**       | Can cause unnecessary re-renders in large trees | Optimized for large apps, avoids unnecessary re-renders |
| **Debugging Tools**   | Limited                                   | Advanced (Redux DevTools)                  |
| **Boilerplate**       | Low                                       | High (actions, reducers, store)            |
| **Learning Curve**    | Low                                       | Higher                                     |

---

### **How They Work**

- **Context API:**  
  - Enables sharing data across components without prop drilling.
  - Uses `Provider` to supply data and `Consumer` to access it.
  - Best for global data like theme, user, or locale.

- **Redux:**  
  - Maintains all app state in a single store.
  - State changes are handled via actions and reducers for predictability.
  - Supports middleware, time-travel debugging, and is easier to test in large apps.

---

### **When to Use Each**

- **Context API:**  
  - Simple or infrequently changing global state.
  - Avoiding prop drilling in small/medium projects.
  - Minimal setup and boilerplate needs.

- **Redux:**  
  - Complex, frequently changing state across many components.
  - Large-scale applications needing strict state control, performance optimization, and advanced debugging.

---

### **Performance Consideration**

- **Context API** can cause unnecessary re-renders for all consuming components when the context value changes, which may impact performance in large apps.
- **Redux** uses selectors and connect functions to optimize and minimize re-renders, updating only components that need it.

---

### **Summary Table**

| Feature          | Context API                         | Redux                                   |
|------------------|-------------------------------------|-----------------------------------------|
| Architecture     | Decentralized                       | Centralized                             |
| Boilerplate      | Minimal                             | High                                    |
| Performance      | Good for small apps                 | Optimized for large/complex apps        |
| Debugging        | Basic                               | Advanced (DevTools)                     |
| Use Case         | Simple/global state                 | Complex/shared state                    |

---

**In summary:**  
Context API is simple and best for smaller apps or simple global state, while Redux is more powerful and suited for large, complex applications requiring robust state management, performance optimization, and advanced debugging tools.

#  3. Default behavior of useEffect() with empty dependency array?
**Runs only once after first render.**

When you use the `useEffect` hook in React with an **empty dependency array** (`[]`), the effect runs **only once after the first render** of the component—this is commonly referred to as "on mount" behavior.

### **Key Points**

- **Runs only once:** The effect executes after the initial render, similar to the `componentDidMount` lifecycle method in class components.
- **No dependencies:** By providing an empty array, you tell React that the effect does not depend on any props or state, so it should not re-run on subsequent renders.
- **Common use cases:** Fetching data when the component mounts, setting up subscriptions, or initializing values that should only be set once.

### **Example**
```js
useEffect(() => {
// This code runs only once after the first render
fetchData();
}, []); // Empty array as dependency
```

### **Summary Table**

| Dependency Array | When useEffect Runs                |
|------------------|------------------------------------|
| Not provided     | After every render                 |
| [] (empty array) | Only once, after first render      |
| [dep1, dep2]     | After first render and when any dependency changes |

**Conclusion:**  
Yes, `useEffect` with an empty dependency array runs only once after the first render.

# 4. Which property to use to conditionally render routes in react router?
## React Router v6: Key Props and Their Usage

React Router v6 offers a streamlined API for defining routes and navigation in React applications. Here are the main props and their usage for the most commonly used components:

---

### **1. `<Route>` Component Props**

| Prop        | Type           | Usage & Description                                                                                   |
|-------------|----------------|------------------------------------------------------------------------------------------------------|
| `path`      | string         | The URL path to match. Example: `path="/about"`                                                      |
| `element`   | ReactElement   | The React element (component) to render when the path matches. Example: `element={<About />}`        |
| `children`  | Route(s)       | Nested routes for creating route hierarchies.                                                        |
| `index`     | boolean        | Marks the route as the default child route (index route) for its parent.                             |

**Example:**
```js
<Route path="/about" element={<About />} />
<Route path="/users/:id" element={<UserProfile />} />
<Route index element={<Home />} /> // Index route
```
---

### **2. `<Routes>` Component**

- **Usage:** Wraps multiple `<Route>` components. Renders the first child `<Route>` that matches the current URL.
- **Props:** No special props; it simply acts as a container for `<Route>`s.

---

### **3. `<RouterProvider>` Component**

| Prop      | Type      | Usage & Description                                                        |
|-----------|-----------|----------------------------------------------------------------------------|
| `router`  | object    | The router object created with `createBrowserRouter` or similar functions. |

**Example:**
```js
import { RouterProvider } from 'react-router-dom';
<RouterProvider router={router} />
```
---

### **4. `<Link>` and `<NavLink>` Components**

| Prop         | Type              | Usage & Description                                                                                  |
|--------------|-------------------|-----------------------------------------------------------------------------------------------------|
| `to`         | string/object     | The destination path or location object. Example: `to="/about"`                                      |
| `replace`    | boolean           | If `true`, replaces the current entry in the history stack instead of adding a new one.              |
| `state`      | any               | Pass state to the destination route.                                                                 |
| `className`  | string/function   | Sets the class; can be a function to set class based on active state (for `<NavLink>`).              |
| `style`      | object/function   | Sets the style; can be a function to set style based on active state (for `<NavLink>`).              |

**Example:**
```js
<Link to="/about">About</Link> <NavLink to="/home" className={({ isActive }) => isActive ? "active" : ""}>Home</NavLink>
```
---
### **5. Route Matching and Dynamic Segments**

Dynamic Segments: Use :param in the path to match dynamic values.
```js
<Route path="/user/:userId" element={<UserProfile />} />
```
Accessing Params: Use the useParams hook inside the component.
```js
const { userId } = useParams();
```
### **6. Other Useful Props/Features**

- No More exact: All routes match exactly by default in v6; no need for the exact prop.

- No More component or render: Use element instead to specify the component directly.

- Nested Routes: Define nested routes using the children prop or by nesting <Route> elements inside each other.

**There's no special property — just use JavaScript logic.**

# 5. Correct Way to Bind a Function in a Class Component (React)

Binding functions in React class components ensures that the `this` keyword correctly refers to the class instance when the function is called. There are several approaches, but some are more efficient and recommended than others.

---

### **Recommended Approaches**

#### **1. Bind in the Constructor (Classic & Efficient)**

This is the most traditional and performance-friendly method, as the binding happens once when the component is created.

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    // 'this' refers to the class instance
  }

  render() {
    return Click Me;
  }
}
```
- **Pros:** Efficient; the function is not re-created on every render.
- **Cons:** Slightly more boilerplate code.

---

#### **2. Class Property Arrow Function (Modern & Concise)**

With class fields syntax (supported by Babel and modern JS), you can use arrow functions to auto-bind methods:

```js
class MyComponent extends React.Component {
  handleClick = () => {
    // 'this' refers to the class instance
  };

  render() {
    return Click Me;
  }
}
```
- **Pros:** Cleaner syntax; no need to bind in constructor; avoids re-creating functions on each render.
- **Cons:** Requires class fields proposal support (most modern setups have this).

---

### **Approaches to Avoid**

#### **Binding in Render (Anti-pattern for Performance)**

```js
render() {
  return Click Me;
}
```
- **Cons:** Creates a new function on every render, which can hurt performance, especially in large lists or frequent renders.

---

### **Summary Table**

| Method                | Syntax Example                            | Performance | Recommendation         |
|-----------------------|-------------------------------------------|-------------|------------------------|
| Constructor Binding   | `this.method = this.method.bind(this);`   | Good        | Recommended (Classic)  |
| Arrow Function Field  | `method = () => {}`                       | Good        | Recommended (Modern)   |
| Bind in Render        | `onClick={this.method.bind(this)}`        | Poor        | Not Recommended        |

---

**In summary:**  
- **Best practice:** Bind functions in the constructor or use class property arrow functions.
- **Avoid:** Binding in the render method, as it creates a new function on every render and can impact performance.


# 6. Hook to share logic acrosee multiple conponents?
Custom hooks.

## Hook to Share Logic Across Multiple Components in React

The correct answer is **custom hook**.

### **Explanation**

- **Custom hooks** allow you to extract and reuse logic across multiple components in React.  
- You create a custom hook by defining a function that starts with `use`, and inside it, you can use other hooks like `useState`, `useEffect`, etc.
- This lets you encapsulate logic (such as fetching data, handling forms, counters, etc.) and share it easily between different components without duplicating code.

---

### **Example**

```js
// useCounter.js
import { useState } from 'react';

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);
  const increment = () => setCount(c => c + 1);
  const decrement = () => setCount(c => c - 1);
  return { count, increment, decrement };
}

export default useCounter;
```

```js
// In any component
import useCounter from './useCounter';

function CounterComponent() {
  const { count, increment, decrement } = useCounter();
  return (
    <>
      {count}
    <button onClick={increment}>+</button>
    <button onClick={decrement}>-</button>
    
  );
}
```

---

### **Summary Table**

| Option         | Can it share logic across components? | Explanation                                                      |
|----------------|--------------------------------------|------------------------------------------------------------------|
| `custom hook`  | Yes                                  | Designed for sharing and reusing logic between components        |
| `useLogic`     | No                                   | Not a real or standard React hook                                |
| Other hooks    | No                                   | Built-in hooks solve specific problems, not for sharing logic    |

---

**In summary:**  
To share logic across multiple React components, use a **custom hook**.

# 7. How to define a prop type for an array of strings?
```markdown
## How to Define a Prop Type for an Array of Strings in React

You can define a prop type for an array of strings in React using either **PropTypes** (for JavaScript) or **TypeScript**.

---

### **1. Using PropTypes (JavaScript)**

Import the `prop-types` package and use `PropTypes.arrayOf(PropTypes.string)`:

```js
import PropTypes from 'prop-types';

MyComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.string).isRequired,
};
```
- This ensures the `items` prop is an array where every element is a string.

---

### **2. Using TypeScript**

Define the prop type in your interface or type alias:

```js
type MyComponentProps = {
  items: string[];
};

const MyComponent: React.FC = ({ items }) => (
  
    {items.map(item => {item})}
  
);
```
- Here, `items: string[]` specifies that `items` must be an array of strings.

---

### **Summary Table**

| Approach      | Syntax Example                                      | Description                       |
|---------------|-----------------------------------------------------|-----------------------------------|
| PropTypes     | `PropTypes.arrayOf(PropTypes.string)`               | JavaScript runtime check          |
| TypeScript    | `items: string[]`                                   | Compile-time type check           |

---

**In summary:**  
- Use `PropTypes.arrayOf(PropTypes.string)` for PropTypes.
- Use `string[]` in TypeScript to define a prop as an array of strings.

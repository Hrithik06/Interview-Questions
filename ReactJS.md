## 1. Avoid unnecessary re-renders in Functional Component.
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

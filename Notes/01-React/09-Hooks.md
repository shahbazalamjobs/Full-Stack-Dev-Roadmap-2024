Certainly! Let's start by explaining the basic hooks in React, namely `useState` and `useEffect`, followed by some example code.

### useState

`useState` is a hook that lets you add React state to function components. When you call `useState`, it returns an array with two elements:

1. The current state value.
2. A function that lets you update the state.

Here's how you can use it:

```jsx
import React, { useState } from 'react';

function Counter() {
  // Declare a state variable named "count" with an initial value of 0
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      {/* When the button is clicked, update the state */}
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default Counter;
```

### Explanation:

- `useState(0)` initializes the state variable `count` with the value `0`.
- `setCount` is a function that you can call to update the state.
- Each time you call `setCount`, the component re-renders with the new state value.

### useEffect

`useEffect` is a hook that lets you perform side effects in function components. It serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in React classes.

Here's an example:

```jsx
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  // useEffect hook
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;

    // Cleanup function
    return () => {
      // Cleanup code if any, runs before the effect is re-applied or component is unmounted
      console.log('Cleaning up...');
    };
  }, [count]); // Dependency array

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default Counter;
```

### Explanation:

- `useEffect` accepts a function that contains the side effect code. This function runs after the component renders.
- The second argument to `useEffect` is the dependency array `[count]`. The effect runs only when the `count` value changes. If you omit this array, the effect runs after every render.
- The function can return a cleanup function. This cleanup function runs before the effect is re-applied and when the component is unmounted.

### Full Example

Combining both hooks in a single component:

```jsx
import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
    return () => {
      console.log('Cleaning up...');
    };
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default Counter;
```

### Summary

- `useState` adds state to functional components.
- `useEffect` handles side effects in functional components.
- Hooks can be used in combination to manage state and side effects effectively in your React applications.

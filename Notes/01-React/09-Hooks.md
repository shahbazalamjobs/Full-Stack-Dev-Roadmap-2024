
# Hooks


Certainly! Let's focus on the `useState` hook:

# 1. useState Hook

The `useState` hook is a built-in React hook that allows functional components to manage state. It returns an array with two elements:

1. The current state value.
2. A function to update the state.

#### Basic Syntax

```jsx
const [state, setState] = useState(initialValue);
```

- `state`: Represents the current state value.
- `setState`: Function used to update the state.
- `initialValue`: Initial value for the state.

#### Example

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

#### Explanation

- `useState(0)` initializes the state variable `count` with the value `0`.
- `setCount` is a function that you can call to update the state.
- Each time you call `setCount`, the component re-renders with the new state value.

#### Summary

- `useState` allows functional components to manage state.
- It returns an array with the current state value and a function to update the state.
- You can call the update function to change the state, triggering a re-render of the component.

Certainly! Let's dive deeper into the `useEffect` hook, covering its usage, cleanup mechanism, and advanced scenarios.

---


# 2. Usage of `useEffect`

The `useEffect` hook allows you to perform side effects in your function components. Side effects can be data fetching, subscriptions, or manually changing the DOM (like updating the document title).

#### Basic Syntax

```jsx
useEffect(() => {
  // Effect code here
  return () => {
    // Optional cleanup code here
  };
}, [dependencies]);
```

- **Effect Function**: This is the main function that contains your side-effect logic. It runs after the render.
- **Cleanup Function**: This is optional and is used for cleaning up side effects (e.g., clearing timers, canceling network requests, etc.). It runs before the effect is re-applied and when the component unmounts.
- **Dependency Array**: This array specifies the dependencies that trigger the effect. The effect runs only when one of these dependencies changes.

### No Dependency Array

If you omit the dependency array, the effect runs after every render:

```jsx
useEffect(() => {
  console.log('Effect runs after every render');
});
```

### Empty Dependency Array

If you provide an empty array, the effect runs only once, after the initial render:

```jsx
useEffect(() => {
  console.log('Effect runs only once, after the initial render');
}, []);
```

### With Dependencies

The effect runs only when the specified dependencies change:

```jsx
useEffect(() => {
  console.log('Effect runs when count changes');
}, [count]);
```

### Cleanup Function

The cleanup function is used to clean up side effects. It runs before the effect re-runs and when the component unmounts.

Example with a timer:

```jsx
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  }, []);

  return <div>Seconds: {seconds}</div>;
}

export default Timer;
```

### Detailed Explanation:

1. **Effect Function**: The `setInterval` function starts a timer that increments the `seconds` state every second.
2. **Cleanup Function**: The `clearInterval` function stops the timer when the component unmounts or before the effect re-runs.

### Multiple Effects

You can use multiple `useEffect` hooks in a single component. Each `useEffect` hook is independent and can handle different side effects:

```jsx
import React, { useState, useEffect } from 'react';

function MultiEffectComponent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  useEffect(() => {
    console.log('Count effect:', count);
  }, [count]);

  useEffect(() => {
    console.log('Text effect:', text);
  }, [text]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <p>Text: {text}</p>
      <input value={text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
}

export default MultiEffectComponent;
```

### Advanced Scenarios

#### Fetching Data

You can use `useEffect` to fetch data from an API when the component mounts:

```jsx
import React, { useState, useEffect } from 'react';

function DataFetcher() {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchData() {
      const response = await fetch('https://api.example.com/data');
      const result = await response.json();
      setData(result);
      setLoading(false);
    }

    fetchData();
  }, []);

  if (loading) {
    return <div>Loading...</div>;
  }

  return (
    <div>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}

export default DataFetcher;
```

#### Cleanup with Subscriptions

When dealing with subscriptions (e.g., WebSocket connections), you can set up and clean up within the `useEffect`:

```jsx
import React, { useEffect } from 'react';

function WebSocketComponent() {
  useEffect(() => {
    const socket = new WebSocket('ws://example.com/socket');

    socket.onopen = () => {
      console.log('WebSocket Connected');
    };

    socket.onmessage = (event) => {
      console.log('Message from server', event.data);
    };

    return () => {
      socket.close();
    };
  }, []);

  return <div>WebSocket Example</div>;
}

export default WebSocketComponent;
```

### Summary

- **Effect Function**: Runs your side-effect logic after rendering.
- **Cleanup Function**: Cleans up the effect, runs before the next effect or component unmount.
- **Dependency Array**: Controls when the effect runs, based on changes to specified dependencies.
- `useEffect` is powerful for managing side effects in function components, replacing the lifecycle methods in class components, and promoting a more functional approach to React development.


---


# 3. `useCallback`

### What is useCallback?

- useCallback is a React hook used to memoize functions.
- It returns a memoized version of the callback function that only changes if one of the dependencies has changed.
- It's useful for optimizing performance by avoiding unnecessary re-renders in child components.

```jsx
import React, { useState, useCallback } from 'react';

const Button = ({ onClick, children }) => {
  console.log('Button rendering');
  return <button onClick={onClick}>{children}</button>;
};

const ParentComponent = () => {
  const [count, setCount] = useState(0);

  // Define a callback function using useCallback
  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]); // Dependency is count

  return (
    <div>
      <h1>Count: {count}</h1>
      <Button onClick={handleClick}>Increment</Button>
    </div>
  );
};

export default ParentComponent;
```

Explanation:

- `handleClick` is a callback function that increments the `count` state by 1.
- It is memoized using `useCallback`. The callback is recreated only when the `count` state changes.
- The `Button` component receives `onClick` as a prop, which is the memoized `handleClick` function. This ensures that `Button` does not re-render unnecessarily when the `count` changes, optimizing performance.



---

# 4. `useReducer` hook in React:

1. **What is `useReducer`?**
   - `useReducer` is one of the built-in React hooks used for state management.
   - It is an alternative to `useState` for managing more complex state logic.
   - It accepts a reducer function and an initial state as arguments and returns the current state and a dispatch function.

2. **Syntax:**
   ```javascript
   const [state, dispatch] = useReducer(reducer, initialState);
   ```

   - `reducer`: A function that takes the current state and an action as arguments and returns a new state based on the action. It follows the signature `(state, action) => newState`.
   - `initialState`: The initial state of the component.

3. **Example:**
   ```javascript
   import React, { useReducer } from 'react';

   const initialState = { count: 0 };

   const reducer = (state, action) => {
     switch (action.type) {
       case 'increment':
         return { count: state.count + 1 };
       case 'decrement':
         return { count: state.count - 1 };
       default:
         throw new Error();
     }
   };

   const Counter = () => {
     const [state, dispatch] = useReducer(reducer, initialState);

     return (
       <div>
         Count: {state.count}
         <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
         <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
       </div>
     );
   };

   export default Counter;
   ```

4. **When to use `useReducer`?**
   - `useReducer` is useful when the state logic is complex or involves multiple sub-values.
   - It's a good choice when the next state depends on the previous one and requires more than a simple update.

5. **Benefits:**
   - It provides a centralized way to manage state updates, making the code more predictable and easier to debug.
   - It facilitates managing complex state transitions and logic.

6. **Drawbacks:**
   - It may be overkill for managing simple state updates, where `useState` might be more appropriate.
   - The initial setup and understanding of reducers might be more complex compared to `useState`.


# Hooks


Certainly! Let's focus on the `useState` hook:

### useState Hook

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


### Usage of `useEffect`

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

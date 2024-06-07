
# Life Cycle Methods

In React functional components, lifecycle methods are handled using hooks, primarily `useEffect`. Here’s a comprehensive guide on how to replicate common lifecycle methods in functional components.

### 1. `componentDidMount` Equivalent
To run code once after the component mounts, you use `useEffect` with an empty dependency array:

```jsx
import React, { useEffect } from 'react';

function ComponentDidMountExample() {
  useEffect(() => {
    // This code runs once after the component mounts
    console.log('Component did mount');

    // Cleanup function runs on component unmount
    return () => {
      console.log('Component will unmount');
    };
  }, []);

  return <div>Component Did Mount Example</div>;
}

export default ComponentDidMountExample;
```

### 2. `componentDidUpdate` Equivalent
To run code after the component updates, you include dependencies in the array. The effect runs whenever any of these dependencies change:

```jsx
import React, { useState, useEffect } from 'react';

function ComponentDidUpdateExample() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // This code runs after the component updates
    console.log('Component did update');

    // Optional cleanup function
    return () => {
      console.log('Cleanup before update');
    };
  }, [count]); // Only re-run the effect if count changes

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default ComponentDidUpdateExample;
```

### 3. `componentWillUnmount` Equivalent
To run code before the component unmounts, you return a cleanup function from `useEffect`:

```jsx
import React, { useEffect } from 'react';

function ComponentWillUnmountExample() {
  useEffect(() => {
    // Effect runs on mount
    console.log('Component mounted');

    // Cleanup function runs on unmount
    return () => {
      console.log('Component will unmount');
    };
  }, []); // Empty dependency array means this effect only runs on mount and unmount

  return <div>Component Will Unmount Example</div>;
}

export default ComponentWillUnmountExample;
```

### 4. Combining All Lifecycle Methods
You can combine all these lifecycle behaviors within a single `useEffect` by mixing the usage of dependencies and cleanup functions:

```jsx
import React, { useState, useEffect } from 'react';

function CombinedLifecycleExample() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Runs on mount and updates
    console.log('Component did mount or update');

    // Cleanup before the next effect run or before unmount
    return () => {
      console.log('Cleanup before update or unmount');
    };
  }, [count]); // Dependency array to control when the effect runs

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default CombinedLifecycleExample;
```

### 5. `useEffect` for Fetching Data (Side Effects)
For data fetching and other side effects:

```jsx
import React, { useState, useEffect } from 'react';

function FetchDataExample() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Function to fetch data
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/data');
        const result = await response.json();
        setData(result);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    fetchData();
  }, []); // Empty dependency array means this runs once after mount

  return (
    <div>
      <pre>{data ? JSON.stringify(data, null, 2) : 'Loading...'}</pre>
    </div>
  );
}

export default FetchDataExample;
```

### Summary
- **`componentDidMount`**: Use `useEffect` with an empty dependency array (`[]`).
- **`componentDidUpdate`**: Use `useEffect` with dependencies listed in the array.
- **`componentWillUnmount`**: Return a cleanup function from `useEffect`.
- **Combining Lifecycle Methods**: Mix dependencies and cleanup functions in `useEffect`.
- **Side Effects (Data Fetching)**: Use `useEffect` to handle asynchronous operations like fetching data.

These examples cover the equivalents of class component lifecycle methods in functional components using React hooks.

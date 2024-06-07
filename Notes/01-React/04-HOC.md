# High Order Component

Certainly! Higher-Order Components (HOCs) are a pattern in React that allows you to reuse component logic. They are functions that take a component and return a new component with additional features or functionality. HOCs are a powerful tool for code reuse and abstraction in React applications.

Let's go through the code and explanation of creating a Higher-Order Component (HOC) in a functional component:

### Definition:
A Higher-Order Component is a function that takes a component and returns a new component with enhanced functionality.

### Usage:
You can use a HOC to add common functionalities like logging, authentication, or data fetching to multiple components without duplicating code.

### Reusability:
HOCs allow you to extract common logic from components, making it easier to reuse across your application. For example, if you have multiple components that require authentication, you can create a HOC for handling authentication and use it with those components.

- Example of a Higher-Order Component (HOC) that adds a "loading" state to any component it wraps. This HOC will display a loading message until the wrapped component is fully loaded.

```jsx
import React, { useState, useEffect } from 'react';

// Define a Higher-Order Component
const withLoading = (WrappedComponent) => {
  // Define a new component
  const WithLoading = (props) => {
    const [isLoading, setIsLoading] = useState(true);

    useEffect(() => {
      // Simulate loading time
      const timer = setTimeout(() => {
        setIsLoading(false);
      }, 2000);

      // Clean up timer
      return () => clearTimeout(timer);
    }, []);

    // If loading, display loading message
    if (isLoading) {
      return <div>Loading...</div>;
    }

    // Once loaded, render the wrapped component with its props
    return <WrappedComponent {...props} />;
  };

  // Return the new component
  return WithLoading;
};

// Define a simple functional component
const MyComponent = () => {
  return <div>Hello World!</div>;
};

// Enhance the component with the loading HOC
const MyComponentWithLoading = withLoading(MyComponent);

// Usage: Render the enhanced component
const App = () => {
  return (
    <div>
      <MyComponentWithLoading />
    </div>
  );
};

export default App;
```

Explanation:

- We create a Higher-Order Component called `withLoading` that takes a `WrappedComponent` as an argument.
- Inside `withLoading`, we define a new component `WithLoading`.
- `WithLoading` component initializes a state `isLoading` to track loading status.
- We use `useEffect` to simulate a loading time of 2 seconds and then update the `isLoading` state to `false`.
- While the component is loading (`isLoading` is `true`), we display a loading message. Once loading is complete, we render the wrapped component (`WrappedComponent`).
- Finally, we enhance our `MyComponent` by passing it to `withLoading`, resulting in `MyComponentWithLoading`.
- In the `App` component, we render `MyComponentWithLoading`.

This example demonstrates a simple use case of a Higher-Order Component to add loading functionality to any component it wraps.

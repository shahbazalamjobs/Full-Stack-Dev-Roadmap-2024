# `PureComponent` (class-based) and `React.memo()` with `useMemo()` (functional-based) 

- Used for optimizing performance in React components.

### Class-based Component with `PureComponent`:

#### Summary:
- `PureComponent` is a base class for React components that implements `shouldComponentUpdate` with a shallow prop and state comparison.
- It optimizes performance by preventing unnecessary re-renders, only updating when props or state change.

#### Code Example:
```jsx
import React, { PureComponent } from 'react';

class MyPureComponent extends PureComponent {
  render() {
    return <div>{this.props.someData}</div>;
  }
}
```

### Functional Component with `React.memo()` and `useMemo()`:

#### Summary:
- `React.memo()` is a higher-order component used to memoize the result of a functional component based on its props.
- `useMemo()` is a hook used to memoize the result of expensive calculations inside a functional component.

#### Code Example:
```jsx
import React, { useMemo } from 'react';

const MyFunctionalComponent = React.memo(({ someData }) => {
  const memoizedData = useMemo(() => {
    // Expensive calculations based on props
    return someData;
  }, [someData]);

  return <div>{memoizedData}</div>;
});
```

In summary, both approaches provide ways to optimize performance in React components, with class-based `PureComponent` offering automatic shallow comparison of props and state, while functional components leverage `React.memo()` and `useMemo()` to achieve similar optimization by memoizing the result of expensive calculations. Choose the approach that best fits your project's requirements and coding style.

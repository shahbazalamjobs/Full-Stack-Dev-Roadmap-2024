Certainly! Here's an example of each of the mentioned methods for conditional rendering in React:

### 1. Using If/Else Statements:
```jsx
function Component({ isLoggedIn }) {
  if (isLoggedIn) {
    return <UserGreeting />;
  } else {
    return <GuestGreeting />;
  }
}
```

### 2. Ternary Operators:
```jsx
function Component({ isLoggedIn }) {
  return isLoggedIn ? <UserGreeting /> : <GuestGreeting />;
}
```

### 3. Logical && Operator:
```jsx
function Component({ isLoggedIn }) {
  return isLoggedIn && <UserGreeting />;
}
```

### 4. Switch Case:
```jsx
function Component({ status }) {
  switch (status) {
    case 'loading':
      return <Loading />;
    case 'success':
      return <Success />;
    case 'error':
      return <Error />;
    default:
      return null;
  }
}
```

### 5. Inline If-Else with Conditional Operator:
```jsx
function Component({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? (
        <UserGreeting />
      ) : (
        <GuestGreeting />
      )}
    </div>
  );
}
```

These examples demonstrate different ways to conditionally render components in React, depending on the value of a given prop (`isLoggedIn` or `status`). Each method has its use case and can be chosen based on readability, simplicity, and specific requirements of the application.

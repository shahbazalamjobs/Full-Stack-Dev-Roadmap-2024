
# Context API with functional components in React.

```jsx
import React, { createContext, useContext, useState } from 'react';

// Creating Context
const ThemeContext = createContext();

// Providing Context
const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme(prevTheme => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

// Consuming Context
const ThemeConsumer = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <div>
      <p>Current Theme: {theme}</p>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </div>
  );
};

// Context with Class Components (Optional)
// You can use ThemeContext.Consumer instead of ThemeConsumer component

// Updating Context
// You can update the context value directly inside a functional component using useState
// Or using a class component, you can use ThemeContext.Consumer or static contextType

const App = () => {
  return (
    <ThemeProvider>
      <div>
        <h1>Theme Toggler</h1>
        <ThemeConsumer />
      </div>
    </ThemeProvider>
  );
};

export default App;
```

Explanation:

1. **Creating Context**: The `createContext` function is used to create a context object. This context object will be used to share data between components.

2. **Providing Context**: The `ThemeProvider` component is created to provide the context to its child components. It wraps its children with `ThemeContext.Provider` and passes down the `theme` and `toggleTheme` values using the `value` prop.

3. **Consuming Context**: The `ThemeConsumer` component consumes the context using the `useContext` hook. It retrieves the `theme` and `toggleTheme` values from the context and uses them to render UI elements.

4. **Context with Class Components (Optional)**: If you want to use context with class components, you can use `ThemeContext.Consumer` or the `static contextType` property.

5. **Updating Context**: You can update the context value directly inside functional components using `useState`. In class components, you can update the context value using `ThemeContext.Consumer` or `static contextType`.

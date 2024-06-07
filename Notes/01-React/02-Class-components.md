### Class Components in React

Class components are one of the ways to define components in React. They are more powerful than functional components in that they can hold and manage local state, and have access to lifecycle methods.

#### Definition
A class component is a JavaScript class that extends `React.Component` and implements a `render` method which returns React elements.

#### Example:
```jsx
import React, { Component } from 'react';

class Greeting extends Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
      </div>
    );
  }
}

export default Greeting;
```

### Lifecycle Methods
Class components have several lifecycle methods that can be overridden to run code at specific times during the component's lifecycle.

#### Example:
```jsx
import React, { Component } from 'react';

class Timer extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    this.interval = setInterval(() => {
      this.setState({ count: this.state.count + 1 });
    }, 1000);
  }

  componentWillUnmount() {
    clearInterval(this.interval);
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
      </div>
    );
  }
}

export default Timer;
```

### State Management
State is a way to manage data that changes over time in a component.

#### Example:
```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

### Props Handling
Props are inputs to components. They are passed to the component via HTML attributes.

#### Example:
```jsx
import React, { Component } from 'react';

class DisplayMessage extends Component {
  render() {
    return <p>{this.props.message}</p>;
  }
}

export default DisplayMessage;

// Usage in another component
import React from 'react';
import DisplayMessage from './DisplayMessage';

const App = () => (
  <div>
    <DisplayMessage message="Hello, world!" />
  </div>
);

export default App;
```

### Component Methods
Component methods are custom methods defined within a class component to handle various operations like events or computations.

#### Example:
```jsx
import React, { Component } from 'react';

class Toggle extends Component {
  constructor(props) {
    super(props);
    this.state = { isOn: true };
  }

  toggle = () => {
    this.setState({ isOn: !this.state.isOn });
  };

  render() {
    return (
      <div>
        <p>{this.state.isOn ? 'ON' : 'OFF'}</p>
        <button onClick={this.toggle}>Toggle</button>
      </div>
    );
  }
}

export default Toggle;
```

### Summary
- **Definition**: Class components extend `React.Component` and implement a `render` method.
- **Lifecycle Methods**: Methods like `componentDidMount` and `componentWillUnmount` to run code at specific times.
- **State Management**: Manage dynamic data with `this.state` and `this.setState`.
- **Props Handling**: Receive data through `this.props`.
- **Component Methods**: Custom methods to handle events and operations within the component.


# Hooks

Certainly! Below are examples of how to handle state in functional components using hooks (particularly `useState`) in React.

### 1. State Initialization and Updating State
Here's a simple example of initializing state and updating it:

```jsx
import React, { useState } from 'react';

function Counter() {
  // State Initialization
  const [count, setCount] = useState(0);

  // Function to update the state
  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

### 2. Using Multiple State Variables
You can manage multiple state variables within a single functional component:

```jsx
import React, { useState } from 'react';

function UserInfo() {
  // Multiple State Variables
  const [name, setName] = useState('');
  const [age, setAge] = useState(0);

  return (
    <div>
      <p>Name: {name}</p>
      <input 
        type="text" 
        value={name} 
        onChange={(e) => setName(e.target.value)} 
        placeholder="Enter your name" 
      />
      <p>Age: {age}</p>
      <input 
        type="number" 
        value={age} 
        onChange={(e) => setAge(parseInt(e.target.value, 10))} 
        placeholder="Enter your age" 
      />
    </div>
  );
}

export default UserInfo;
```

### 3. Derived State
Sometimes, you may want to derive state from other states. For example:

```jsx
import React, { useState } from 'react';

function DerivedState() {
  const [price, setPrice] = useState(0);
  const [quantity, setQuantity] = useState(0);

  // Derived State
  const total = price * quantity;

  return (
    <div>
      <p>Price: {price}</p>
      <input 
        type="number" 
        value={price} 
        onChange={(e) => setPrice(parseFloat(e.target.value))} 
        placeholder="Enter price" 
      />
      <p>Quantity: {quantity}</p>
      <input 
        type="number" 
        value={quantity} 
        onChange={(e) => setQuantity(parseInt(e.target.value, 10))} 
        placeholder="Enter quantity" 
      />
      <p>Total: {total}</p>
    </div>
  );
}

export default DerivedState;
```

### 4. Complex State with Objects
Sometimes state might need to handle more complex structures like objects:

```jsx
import React, { useState } from 'react';

function UserProfile() {
  const [user, setUser] = useState({
    name: '',
    age: 0,
    email: ''
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setUser(prevUser => ({
      ...prevUser,
      [name]: value
    }));
  };

  return (
    <div>
      <input 
        type="text" 
        name="name" 
        value={user.name} 
        onChange={handleChange} 
        placeholder="Enter your name" 
      />
      <input 
        type="number" 
        name="age" 
        value={user.age} 
        onChange={handleChange} 
        placeholder="Enter your age" 
      />
      <input 
        type="email" 
        name="email" 
        value={user.email} 
        onChange={handleChange} 
        placeholder="Enter your email" 
      />
      <p>Name: {user.name}</p>
      <p>Age: {user.age}</p>
      <p>Email: {user.email}</p>
    </div>
  );
}

export default UserProfile;
```

### Summary
- **State Initialization**: Use `useState` to initialize state variables.
- **Updating State**: Use state setter functions provided by `useState` to update state.
- **Using Multiple State Variables**: Declare multiple state variables using multiple `useState` calls.
- **Derived State**: Calculate derived state directly within the component rendering logic.
- **Complex State with Objects**: Manage complex state structures like objects by updating state in a functional manner.

These examples cover the basics of managing state in functional components using hooks in React.

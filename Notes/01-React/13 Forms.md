Certainly! Let's go through each of these topics related to forms in React.

### Controlled Components:

In controlled components, form data is handled by React components. Input elements receive their current value through props, and React controls what happens in the form.

```jsx
import React, { useState } from 'react';

const MyForm = () => {
  const [value, setValue] = useState('');

  const handleChange = (event) => {
    setValue(event.target.value);
  };

  return (
    <form>
      <input type="text" value={value} onChange={handleChange} />
    </form>
  );
};

export default MyForm;
```

### Uncontrolled Components:

In uncontrolled components, form data is handled by the DOM itself. React does not manage the form data.

```jsx
import React from 'react';

const MyForm = () => {
  let inputRef = React.createRef();

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Input Value:', inputRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={inputRef} />
      <button type="submit">Submit</button>
    </form>
  );
};

export default MyForm;
```

### Handling Form Submissions:

Form submissions can be handled by attaching an `onSubmit` event handler to the form element.

```jsx
import React, { useState } from 'react';

const MyForm = () => {
  const [value, setValue] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Submitted Value:', value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={value} onChange={(e) => setValue(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
};

export default MyForm;
```

### Form Validation:

Form validation can be done by checking the input value against certain criteria, such as length or format.

```jsx
import React, { useState } from 'react';

const MyForm = () => {
  const [value, setValue] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();
    if (value.trim() === '') {
      setError('Input cannot be empty');
    } else {
      setError('');
      console.log('Submitted Value:', value);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={value} onChange={(e) => setValue(e.target.value)} />
      <button type="submit">Submit</button>
      {error && <p>{error}</p>}
    </form>
  );
};

export default MyForm;
```

### Handling Multiple Inputs:

For forms with multiple inputs, you can manage each input's value individually in the state.

```jsx
import React, { useState } from 'react';

const MyForm = () => {
  const [formData, setFormData] = useState({
    username: '',
    email: '',
    password: ''
  });

  const handleChange = (event) => {
    const { name, value } = event.target;
    setFormData({ ...formData, [name]: value });
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form Data:', formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" name="username" value={formData.username} onChange={handleChange} />
      <input type="email" name="email" value={formData.email} onChange={handleChange} />
      <input type="password" name="password" value={formData.password} onChange={handleChange} />
      <button type="submit">Submit</button>
    </form>
  );
};

export default MyForm;
```

### Refs with Forms:

Refs can be used to directly interact with form elements, such as accessing their values or focusing them.

```jsx
import React, { useRef } from 'react';

const MyForm = () => {
  const inputRef = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Input Value:', inputRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={inputRef} />
      <button type="submit">Submit</button>
    </form>
  );
};

export default MyForm;
```

These examples cover the basics of handling forms in React, including controlled and uncontrolled components, form submissions, form validation, handling multiple inputs, and using refs with forms.

Sure, let's dive into the basics of React Router without using older code syntax:

### Setting Up React Router:
To start using React Router, first install it using npm or yarn:

```bash
npm install react-router-dom
```

### Route Configuration:
In your main application file, typically `App.js` or `index.js`, import BrowserRouter and wrap your entire application with it:

```javascript
import { BrowserRouter as Router } from 'react-router-dom';

function App() {
  return (
    <Router>
      {/* Your application components */}
    </Router>
  );
}
```

### Link and NavLink:
Instead of using traditional `<a>` tags for navigation, use `Link` or `NavLink` components from React Router:

```javascript
import { Link, NavLink } from 'react-router-dom';

<Link to="/about">About</Link>

<NavLink to="/contact" activeClassName="active">Contact</NavLink>
```

### Dynamic Routing:
You can set up dynamic routes by defining placeholders in your route path:

```javascript
<Route path="/user/:userId" component={UserDetails} />
```

Access the parameter in your component using `useParams` hook:

```javascript
import { useParams } from 'react-router-dom';

function UserDetails() {
  let { userId } = useParams();

  return <div>User ID: {userId}</div>;
}
```

### Nested Routes:
You can nest routes by defining additional Route components within other Route components:

```javascript
<Route path="/dashboard">
  <Dashboard />
</Route>
```

### Redirection:
Redirect users to another route using the `Redirect` component:

```javascript
import { Redirect } from 'react-router-dom';

<Redirect to="/login" />
```

These basics should get you started with React Router without using the older code syntax!


--- 


Certainly! Below is the complete code with React Router implemented using Link, NavLink, and Navigate, and avoiding the use of Switch:

**App.js**
```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Contact from './components/Contact';
import User from './components/User';
import UserProfile from './components/UserProfile';
import Navbar from './components/Navbar';
import NotFound from './components/NotFound';

const App = () => {
  return (
    <Router>
      <div>
        <Navbar />
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
          <Route path="/user/:id" element={<User />} >
            <Route path="profile" element={<UserProfile />} />
          </Route>
          <Route path="*" element={<NotFound />} />
        </Routes>
      </div>
    </Router>
  );
}

export default App;
```

**Navbar.js**
```javascript
import React from 'react';
import { Link, NavLink } from 'react-router-dom';

const Navbar = () => {
  return (
    <nav>
      <ul>
        <li>
          <NavLink to="/" exact activeClassName="active">Home</NavLink>
        </li>
        <li>
          <NavLink to="/about" activeClassName="active">About</NavLink>
        </li>
        <li>
          <NavLink to="/contact" activeClassName="active">Contact</NavLink>
        </li>
        <li>
          <Link to="/user/123">User Profile</Link>
        </li>
      </ul>
    </nav>
  );
}

export default Navbar;
```

**Home.js**
```javascript
import React from 'react';

const Home = () => {
  return (
    <div>
      <h2>Home Page</h2>
      <p>Welcome to our website!</p>
    </div>
  );
}

export default Home;
```

**About.js**
```javascript
import React from 'react';

const About = () => {
  return (
    <div>
      <h2>About Page</h2>
      <p>This is the about page.</p>
    </div>
  );
}

export default About;
```

**Contact.js**
```javascript
import React from 'react';

const Contact = () => {
  return (
    <div>
      <h2>Contact Page</h2>
      <p>Contact us here.</p>
    </div>
  );
}

export default Contact;
```

**User.js**
```javascript
import React from 'react';
import { useParams, Link, Routes, Route } from 'react-router-dom';
import UserProfile from './UserProfile';

const User = () => {
  let { id } = useParams();
  return (
    <div>
      <h2>User Page</h2>
      <ul>
        <li>
          <Link to={`profile`}>User Profile</Link>
        </li>
      </ul>
      <Routes>
        <Route path="profile" element={<UserProfile />} />
      </Routes>
    </div>
  );
}

export default User;
```

**UserProfile.js**
```javascript
import React from 'react';
import { useParams } from 'react-router-dom';

const UserProfile = () => {
  let { id } = useParams();
  return (
    <div>
      <h3>User Profile</h3>
      <p>User ID: {id}</p>
    </div>
  );
}

export default UserProfile;
```

**NotFound.js**
```javascript
import React from 'react';

const NotFound = () => {
  return (
    <div>
      <h2>404 Not Found</h2>
      <p>Sorry, the page you are looking for does not exist.</p>
    </div>
  );
}

export default NotFound;
```

This setup ensures that you have all the navigation links (`Link`, `NavLink`) and dynamic routing in place, with routes defined in one page (`App.js`) and navigation links in another (`Navbar.js`).

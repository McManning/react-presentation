---

## React Router

* Separate library from React
* Manages "page" transitions on the frontend

Note:
- Will update your browser URL as well as the history as you interact with the app

+++

### Initialization

```jsx
import { BrowserRouter } from 'react-router-dom';

// Assumes application name is the base
// part of location.pathname
const basename = location.pathname.substr(
    0, location.pathname.indexOf('/', 1)
);

ReactDOM.render(
    <BrowserRouter basename={basename}>
        <App/>
    </BrowserRouter>,
    document.getElementById('app')
);
```

Note:
- Wrap your entire application with a `BrowserRouter` Component

+++

### Links

`<Link to>` instead of `<a href>`

```xml
<nav>
    <ul>
        <li>
            <Link to="/">Home</Link>
        </li>
        <li>
            <Link to="/about/">About</Link>
        </li>
        <li>
            <Link to="/users/">Users</Link>
        </li>
    </ul>
</nav>
```

Note:
- Links generate an anchor DOM element
- Updates the URI and browser history state

+++

### Nav Links

Applies active class on route matches

```xml
<NavLink to="/react" activeClassName="is-active">
    React
</NavLink>
```

+++

### Routes

Renders a Component on URI match

```xml
<div>
    <Route exact path="/" component={Home}/>
    <Route path="/news" component={NewsFeed}/>
</div>
```

Note:
- A `Route` is the encapsulating component for a URI match. Meaning that changing the URI does not necessarily change the entire document - only the sections of a document that match the new URI.

+++

### Advanced Routing

Use placeholders for route matching

```jsx
const User = ({match}) => {
    return <h1>Hello {match.params.username}!</h1>;
};

const jsx = (
    <div>
        <Route path="/user/:username" component={User} />

        <Link to="/user/chase">Hi Chase</Link>
        <Link to="/user/Neil">Hi Neil</Link>
    </div>
);
```

+++

### 404 Routing

Use a `<Switch>`

```xml
<Switch>
    <Route path="/" exact component={Home} />
    <Route path="/news" component={NewsFeed}/>
    <Route component={NoMatch} />
</Switch>
```

Note:
- Switch will only select one match out of a group
- Route without a path will always match

+++

### RTFM

https://reacttraining.com/react-router/

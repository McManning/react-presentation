---

## React Components

Independent reusable pieces of UI or functionality

+++

### Simple Components

```javascript
class HelloMessage extends React.Component {
    render() {
        return (
            <div className="hello-message">
                Hello {this.props.name}
            </div>
        );
    }
}

ReactDOM.render(
    <HelloMessage name="Taylor" />,
    document.getElementById('app')
);
```

@[1](Each component class extends `React.Component`)
@[2-8](They implement a `render()` method that defines what is displayed)
@[4-6](JSX syntax is used to define DOM elements to render)
@[4](Use `className` instead of `class` to set element classes)
@[12](Properties passed into the element are available in `this.props`)

Note:

- ReactDOM render is only typically done once for a react-only application.
- Used multiple times only when integrating with a non-React app

+++

### Stateful Components

```javascript
class Timer extends React.Component {
    constructor(props) {
        super(props);
        this.state = { seconds: 0 };
    }

    componentDidMount() {
        this.interval = setInterval(
            () => this.tick(), 1000
        );
    }

    componentWillUnmount() {
        clearInterval(this.interval);
    }

    tick() {
        this.setState(state => ({
            seconds: state.seconds + 1
        }));
    }

    render() {
        return (
            <div>
                Seconds: {this.state.seconds}
            </div>
        );
    }
}

ReactDOM.render(<Timer />, mountNode);
```

@[4](A component can maintain an internal state via `this.state`)
@[7-11](Called when a component is first created)
@[13-15](Called when a component is destroyed)
@[17-21](Call `this.setState` to update `this.state` (never modifying it directly))
@[23-29](An update to `this.state` will trigger a re-render)

+++

### Using Non-React Components

```javascript
class Datepicker extends React.Component {
    constructor(props) {
        super(props);
        this.el = React.createRef();
    }

    render() {
        return (
            <div ref={this.el}></div>
        );
    }

    componentDidMount() {
        this.$picker = $(this.el.current);
        this.$picker.datepicker({
            startDate: '-3d'
        });
    }

    componentWillUnmount() {
        this.$picker.datepicker('destroy');
    }
}
```

@[4](Create a DOM reference object on startup)
@[9](Attach the reference as the `ref` attribute to the DOM element)
@[13-18](Call the reference on mount and execute the plugin on the rendered DOM element in `.current`)
@[20-22](Perform any necessary plugin cleanups on unmount)

+++

### Event Handling

```javascript
class ToggleButton extends React.Component {
    constructor(props) {
        super(props);
        this.state = { on: true };

        this.onToggle = this.onToggle.bind(this);
    }

    onToggle() {
        this.setState({
            on: !this.state.on
        });
    }

    render() {
        return (
            <button onClick={this.onToggle}>
                {this.state.on ? 'On' : 'Off'}
            </button>
        );
    }
}
```

@[6, 9-13](Bind a method that will toggle `state.on` every time it's called)
@[17](Connect to a virtual `onClick` property of an element)

Note:
- To keep a "this" reference in the onToggle method, you need to bind it in the constructor.
- onClick is NOT equivalent to the standard HTML onClick. This does not get rendered to the DOM so it's content security policy safe.
- Every click will change the button state, thus changing the label between "On" and "Off"
- Call `setState` instead of mutating `this.state` directly, otherwise your component will not re-render itself.

+++

### Default Props

Define a set of default values for `this.props` if the implementer does not supply an override

```javascript
class HelloMessage extends React.Component {
    ...
}

HelloMessage.defaultProps = {
    name: 'World'
};
```

Note:

- STRONGLY recommend you always provide a defaultProps for your component and document what each property does.

+++

### Passing Through Children

```xml
<header>
    <SystemAlert />
    <OSUNavbar />

    <nav className="navbar navbar-main">
      <a className="navbar-brand" href="#">
        <div className="navbar-org">Office of Research</div>
        {this.props.title}
      </a>

      {this.props.children}
    </nav>
</header>
```

Note:
- Renderer for a component called "AppHeader"
- children include any DOM elements or React components that are passed into this component

+++

### Passing Through Children

```jsx
ReactDOM.render(
  <AppHeader title="My App">
    <Navbar>
      <NavbarLink href="#">Home</NavbarLink>
    </Navbar>

    <Profile osuid="200275154" />
  </AppHeader>,
  mountNode
);
```

Note:
- Navbar and Profile components replace `this.props.children`

+++

### Not Necessarily UI

```jsx
class MyLogic {
    componentDidMount() {
        // behavior here
    }

    render() {
        return null;
    }
}

ReactDOM.render(
    <App>
        <MyLogic />
        <Navbar>...</Navbar>
        <MyForm />
    </App>,
    mountNode
);
```

Note:
- A component does not need to return UI. Sometimes you can use one for pure logic that needs to be embedded onto a page.
- Example would be a container that listens for DOM events and updates contexts - or does some data crunching with a set of Web Workers
- Plain Javascript classes are still okay - not everything HAS to be a Component


---

## Higher Order Components

* Allows reuse of component logic
* A function that returns a new Component
* Composition over Inheritance

Note:
- Component classes will always extend `React.Component`. You'll never extend a component from another component, or create your own abstraction over `React.Component`. Instead, you'll use HOCs to include common behavior.
- Basically, resist the urge for Object-Oriented things you typically do.

+++

### Example HOC

```jsx
const AsFormPage = (WrappedComponent) => {
    class AsFormPageImpl extends React.Component {
        componentDidMount() {
            // Generic model fetch() logic
        }

        onSubmit() {
            // Generic form submit logic
        }

        onChange() {
            // Generic form field change logic
        }

        render() {
            return (
                <WrappedComponent {...this.props}
                    onChange={this.onChange}
                    onSubmit={this.onSubmit} />
            );
        }
    }

    AsFormPageImpl.displayName = `AsFormPage(${getDisplayName(WrappedComponent)})`;
    AsFormPageImpl.defaultProps = WrappedComponent.defaultProps;

    return AsFormPageImpl;
};
```

Note:
- Often you want to pass props down into the wrapped component
- Setting `displayName` will help with debugging with React Dev Tools

+++

### Example Usage

```jsx
import AsFormPage from 'AsFormPage';

class MyForm {
    render() {
        return (
            <form>
                ...
            </form>
        );
    }
};

export default AsFormPage(MyForm);
```

Note:
- MyForm will now have `onSubmit` and `onChange` properties along with its usual properties.
- On mount, it'll fetch() model data automatically.

+++

### RTFM

https://reactjs.org/docs/higher-order-components.html

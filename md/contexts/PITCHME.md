---

## Context

* Replaces Redux for global state
* A Provider component provides data to one or more Consumers

+++

### Context Object

Transfer properties between components

```jsx
/**
 * Context for global information about a form page.
 *
 * Form fields at various levels of nesting within a page may
 * react to this context's state.
 */
const FormStateContext = React.createContext({
    // Should the form - in its entirety - be replaced by
    // a static printable version (replacing inputs with
    // print-friendly DOM elements)
    isPrintable: false,

    // Is the form - in its entirety - lazy loading
    // content from an external source
    isLazyLoading: true
});
```

+++

### Context Provider

Update a Context from within a Component

```jsx
render() {
    const formState = { isPrintable: false, isLazyLoading: true };

    return (
        <FormStateContext.Provider value={formState}>
            <div className="form-page">
                <MyForm />
            </div>
        </FormStateContext.Provider>
    );
}
```

+++

### Context Consumer

Read the current state of a Context

```xml
<FormStateContext.Consumer>
    {({ isPrintable, isLazyLoading }) => (
        <React.Fragment>
            {isPrintable &&
                <p>{this.props.value}</p>
            }

            {isLazyLoading &&
                <div className="text-lazy-loader-line"></div>
            }

            {!isPrintable && !isLazyLoading &&
                <input type="text" className="form-control"
                    value={this.props.value} />
            }
        </React.Fragment>
    )}
</FormStateContext.Consumer>
```

Note:
- This is a component that renders out either an input, a string value, or a loader element based on the Context values
- Consumer needs to be wrapped by a method that accepts the Context data

+++

## Additional Tips

* Keep your providers and consumers as close as possible
* If you are overusing contexts in an application - refactor your design.
* Keep them small and meaningful

Note:
- "as close as possible" means try not to deep nest them too much.


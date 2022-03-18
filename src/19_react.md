<!-- markdownlint-disable MD001 -->

# React

- [Components](#components)
  - [Class components](#class-components)
  - [Function components](#function-components)
- [Properties (props)](#properties-props)
- [Events](#events)
- [Redux](#redux)

### Components

``` jsx
ReactDOM.render(
    <React.StrictMode>
        <MyClassComponent />
    </React.StrictMode>,
    document.getElementById('root')
);
```

#### Class components

``` jsx
import './MyClassComponent.css';

class MyClassComponent extends React.Component {
    render() {
        return (
            <div>My text</div>
        );
    }
}
export default MyClassComponent;
```

#### Function components

``` jsx
function myFunctionComponent() {
    return '<div>My text</div>'
}
```

### Properties (props)

#### Child component

``` jsx
class MyClassComponent extends React.Component {
    constructor(props) {
        super(props);
    }
    render() {
        return (
            <div>
                <div>{this.props.item.name}</div>
            </div>
        );
    }
}
export default ExpenseEntryItem;
```

#### Parent component

``` jsx
const item = {
    id: 1,
    name: "Peter",
}

ReactDOM.render(
    <React.StrictMode>
        <MyClassComponent item={item} />
    </React.StrictMode>,
    document.getElementById('root')
);
```

### Events

``` jsx
class MyClassComponent extends React.Component {
    click() {
        // ...
    }

    render() {
        return (
            <button onClick={() => this.click()}>
                Click me
            </button>
        );
    }
}
```

### Redux

``` jsx
const store = createStore()

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>,
    document.getElementById('root')
)
```

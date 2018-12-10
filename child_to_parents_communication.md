## Methods

1. make a handler on parents component 
2. pass it as props to child component
3. in child component invoke handler function
4. handler function make some changes on state in parents component

## code

### parents

```js
class Parent extends React.Component {
    constructor(props) {
        super(props)

        // Bind the this context to the handler function
        this.handler = this.handler.bind(this);

        // Set some state
        this.state = {
            messageShown: false
        };
    }

    // This method will be sent to the child component
    handler() {
        this.setState({
            messageShown: true
        });
    }

    // Render the child component and set the action property with the handler as value
    render() {
        return <Child action={this.handler} />
    }
}
```


### child

```js
class Child extends React.Component {
    render() {
        return (
            <div>
                {/* The button will execute the handler function set by the parent component */}
                <Button onClick={this.props.action} />
            </div>
        )
    }
}
```

## Reference 

https://ourcodeworld.com/articles/read/409/how-to-update-parent-state-from-child-component-in-react
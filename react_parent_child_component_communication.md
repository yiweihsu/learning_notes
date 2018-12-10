# Guideline for passing around data between parents and children components in React.js

## For class component: make a handler function on parent component

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

## For function component: pass the prop as parameter

In a functional stateless component, the props are received in the function signature as arguments:

```js
class Parent extends React.Component {
 render () {
  return(
   <Child eyeColor={'blue'} />
  )
 }
}

const Child = (props) => {
  return (
    <div style={{backgroundColor: props.eyeColor}} />
  )
}
```

## The way to pass data as props (props as component parameter)

```js
class App extends React.Component {

    render() {
        return (
            <div className="container">
                <div className="row">
                    <div className="col-xs-10 col-xs-offset-1">
                        <Header/>
                    </div>
                </div>
                <div className="row">
                    <div className="col-xs-10 col-xs-offset-1">
                        <Home name={"Max"} age={27}/>
                    </div>
                </div>
            </div>
        );
    }
}

render(<App />, window.document.getElementById('app'));
```

## pass props through react router 

```js

```

# Reference

https://ourcodeworld.com/articles/read/409/how-to-update-parent-state-from-child-component-in-react
https://medium.com/@PhilipAndrews/react-how-to-access-props-in-a-functional-component-6bd4200b9e0b




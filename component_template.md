## Class component / stateful component


### Creating a class component and export it 

```
import React, { Component } from 'react';

class MyComponent extends Component {
  render() {
    return (
      <div>This is my component.</div>
    );
  }
}

export default MyComponent;
```


### Basic form

```
class MyComponentClass extends React.Component {
  render() {
    return <div>{this.props.name}</div>;
  }
}
```

### Setting initiatial state

```
class Button extends React.Component {
  state = { counter: 1 };
  
  handleClick = () => {
    this.setState({
      counter: this.state.counter + 1 
    });
  };
  
  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.counter}
      </button>
    );
  }
}

ReactDOM.render(<Button />, mountNode);
```

### Using lifecycle hooks

```
class MyComponent extends Component {
  // Executes after the component is rendered for the first time
  componentDidMount() {
    this.setState({myState: 'Florida'});
  }

  render() {
    const {myState} = this.state || {};
    const message = `The current state is ${myState}.`;
    return (
      <div>{message}</div>
    );
  }
}
```

## Functional component / stateless component

```
var MyStatelessComponent = function MyStatelessComponent(props) {
  return React.createElement(
    "div",
    null,
    props.name
  );
}
```


```
const Button = props => (
   `<button className="our_button" onClick={props.onClick}>
      {props.label}
   </button>`
);
```



# Reference

https://medium.freecodecamp.org/how-to-write-your-first-react-js-component-d728d759cabc
https://alligator.io/react/class-components/


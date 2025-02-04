# Passing Functions As Props

## Introduction - Why Are Functions Useful As Props?

In React, we can pass functions as props to child components. We can pass functions as props to child components to allow the child component to call the function in the parent component.

One common use case for passing functions as props is to allow the child component to update the state of the parent component. This is useful when the child component needs to update the state of the parent component based on user input.

We don't have state yet, but we will soon. For now, we will just be passing functions as props to demonstrate how it works and explore the last kind of prop we can pass.

## Alert

Let's say we want to create a button inside our nested component that once clicked will call an alert function that is inside our parent component.

```jsx
function Greeting(props) {
  return (
    <div>
      <button onClick={props.greet}>{props.name}</button>
    </div>
  );
}

function GreetApp() {
  function greet1() {
    alert("WUBBALUBBADUBDUB!");
  }

  function greet2() {
    alert("Get schwifty!");
  }

  function greet3() {
    alert("Snake jazz!");
  }

  return (
    <div>
      <Greeting name="Rick" greet={greet1} />
      <Greeting name="Morty" greet={greet2} />
      <Greeting name="Mr. President" greet={greet2} />
      <Greeting name="Summer" greet={greet3} />
    </div>
  );
}

export default GreetApp;
```

## Changing Components In The Parent Component

This is a more complex example where we pass a function as a prop to a child component that will change the state of the parent component.

This will become far more common when we start using React state in our components.

``` jsx
import React from 'react';

function ClickButton(props) {
  return (
    <button onClick={props.handleClick}>
      Click Me
    </button>
  );
}

function ClickStateApp() {
  function handleClick() {
    document.getElementById("message").innerHTML = "Button was clicked!";
  };

  return (
    <div>
      <ClickButton handleClick={handleClick} />
      <div id="message"></div>
    </div>
  );
}

export default ClickStateApp;
```

## Dynamically Changing Styles

In this example, we pass a function as a prop to a child component that will change the style of the parent component.

``` jsx
import React from 'react';

function ChangeStyle(props) {
  return (
    <p onMouseOver={props.handleHover}>
      Hover over this text to change its color.
    </p>
  );
}

function StylesApp() {
  function (event) {
    event.target.style.color = "blue";
  };

  return (
    <div>
      <ChangeStyle handleHover={changeColor} />
    </div>
  );
}

export default StylesApp;
```

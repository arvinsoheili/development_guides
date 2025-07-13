# React Basics

### What are hooks?
you can add interactivity and maintencment to a react state.

 hooks are funtion that let you hook into react state and life cycle features from component.

first of all you need to import it to your component:
```JavaScript
importReact, { useState } from 'react';
```
then declare a state variable:
```JavaScript
const [state, setState] = useState(initialState)
```
you can provide any name for the variable:
```JavaScript
const [showMenu, setShowMenu] = useState(false);
```

#### useState Creates a state variable with an initial value ------> showMenu
#### useState Create a function to set that state variable's value -------> setShowMenu

function `setShowMenu` is used to update the value of show menu by passing the boolean value to it: `setShowMenu(true)`

### what is state?



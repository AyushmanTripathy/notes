# React JS

### State

-   state is like memory of each component
-   state should be owned by a common parent
-   can be created by `useState` hook

```js
const [state, setState] = useState(initialState);
```

### Immutability

-   states should not be mutated in react
-   reason:

```js
x = 100;
//next render will override the prev x value
setX(0);
```

-   also, setting to same reference that is modified doesn't work
-   because react considers them same and hence no rerender
-   local mutations, mutating object before setting it as state, are fine

### Queueing of state updates

-   react waits unitll for event handlers to finish before processing state updates
-   called `batching`
-   hence value of x will change only by one

```js
setX(x + 1);
setX(x + 1);
```

-   instead changes can be queued
-   gives correct result

```js
setX((x) => x + 1);
setX((x) => x + 1);
```

-   naming convetion, first letter or fullname

### Rendering

-   during inital render, DOM nodes are created
-   rerender is triggered by state changes

1. rendering, is calling the component, whoose state changed
1. commiting, apply operations to make same as last rendered output

### useContext hook

### useReducer hook

-   consolidate state update logic outside componant

```js
const [state, dispatch] = useReducer(reducer, initialState);

//handle events by dispatching actions
dispatch(action);

//reducer function
function reducer(state, action) {
    return newState;
}
```

-   named after the `reduce` array method

```js
//also works for many actions at once
finalState = actions.reduce(reducer, initialState);
```

### Minor things

-   returing null for not rendering anything
-   render if true with `&&` (NOTE: dont use numbers as condition)

```js
<p> ayushman {doLastName && "tripathy"} </p>
```

-   remember, if condition is 0, react will render 0
-   `children` is a prop to get jsx inside the component
-   all events in react propagates upwards, except `onScroll`
-   for changing dynamic name in object

```js
{ ...obj, [key]:value }
```

-   to reset a component, pass different `key`

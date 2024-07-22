# React JS

from [react.dev/learn](https://react.dev/learn)

## State

-   state is like memory of each component
-   state should be owned by a common parent
-   can be created by `useState` hook

```js
const [state, setState] = useState(initialState);
```

## Immutability

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

## Queueing of state updates

-   react waits for event handlers to finish before processing state updates
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
-   to prevent `batching`, use `flushSync`
-   forces to commit the changes before continuing

```js
flushSync(() => setX(10));
```

## Rendering

-   during inital render, DOM nodes are created
-   rerender is triggered by state changes

1. rendering, is calling the component, whoose state changed
1. commiting, change DOM to make same as last rendered output

## Hooks

-   allow you to use react's features
-   called immediately inside a component (not inside conditional or loops)

## useContext hook

-   pass state to entire sub tree
-   adapting to situations
-   creating a context in a file

```js
export const StateContext = createContext(initialState);
```

-   parent has to provide context's value to children

```js
<StateContext.Provider value={stateValue}> .... </StateContext.Provider>
```

-   context can be used in a child by importing it and

```js
const state = useContext(StateContext);
```

-   try passing jsx as children before doing this

## useReducer hook

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

## Combining useReducer and useContext

-   export all state and state updating logic to `StateProvider.js`
-   it would export a `StateProvider` component which excepts children

```jsx
export function StateProvider({ children }) {
    const [state, stateDispatch] = useReducer(initialState, reducer);
    return (
        <StateContext.Provider value={state}>
            <StateDispatchContext.Provider value={stateDispatch}>
                {children}
            </StateDispatchContext>
        </StateContext>
    )
}
```

-   the reducer function will be in the same file
-   this can export `custom hooks`

```js
export const useState = () => useContext(StateContext);
export const useStateDispatch = () => useContext(StateDispatchContext);
```

## useRef

-   remembered information but does not trigger a rerender
-   unlike state, ref is mutable

```js
const ref = useRef(initialValue);
console.log(ref.current); //to use the current value
ref.current += 1;
```

-   best practise is to not use `ref` while rendering
-   used to get DOM elements and use Browsers APIs

```jsx
<div ref={myRef}></div>
```

-   to store multiple references use a `ref callback`
-   here node is DOM element when setting ref and null when deleting node

```jsx
const listRef = useRef(new Map());
function setRef(ele, i) {
    return (node) =>
        node ? listRef.current.set(i, ele) : listRef.current.delete(i);
}

list.map((ele, i) => <div ref={setRef(ele, i)}></div>);
```

-   `canary` feature is the ref callback cleanup function

```
function setRef(node) {
    listRef.current.push(node);
    // callback called when node is removed
    return () => listRef.current.pop();
}
```

-   reference is not shared to other components
-   to give reference use `forwardRef`

```jsx
const Child = forwardRef(({ props, ref }) => <div ref={ref}></div>);

function Parent() {
    const ref = useRef(null);
    // ref has reference to div element
    return <Child ref={ref} />;
}
```

-   `useImperativeHandle` can be used to restrict exposure of ref

## useEffect

-   Effects are functions that run at the end of each commit
-   used to step out of react and syncronise with external systems
-   rendering code is pure, effects have all the impure stuff
-   beware of infinite loops (setting state inside of effect)

```js
useEffect(() => {
    // doing something after the render
    return () => {
        //clean up function
        //runs before calling effect and during dismount
    };
}, [state]);
```

-   2nd arg is a list of states on which effect depends on
-   empty list means run only when component first appears (like 'onMount')
-   not specifing, means run on every rerender
-   effects can also depend on refs
-   effects are called twice duing development, won't happen in production

-   clean up function should reset things in the function
-   like remove listeners, undo css changes, discard network requests
-   when fetching data, beware of `race conditions`
-   for reseting a component's state after props changes, use `key` prop

```jsx
export default Parent({ id }) {
    return <Child id={id} key={id}/>
}
function Child({ id }) {
    const [name, setName] = useState("");
    return <div> {name} has id {id} </div>
}
```

-   here name will be reset to `""` if id changes
-   if you want to change only few states in a component, not all
-   **NOTE** changing state with props is bad, as components should be pure

```jsx
function Compnent({ id }) {
    const [name, setName] = useState("");
    const [prevId, setPrevId] = useState(id);
    if (prevId != id) {
        setName("");
        setPrevId(id);
    }
}
```

## useMemo

-   used to cache expensive calculations

```js
function Component({ prop }) {
    const [state, setState] = useState("");

    // calculated when state or prop changes
    const res = expensiveFunc(prop);

    // calculated when only prop changes
    const res = useMemo(() => expensiveFunc(prop), [prop]);
}
```

-   this called function should be pure
-   performance can be checked by cpu throttling

## Minor things

-   run code once when application starts

```js
if (typedef window != "undefined") {
    //once before application starts
}

function App() {
```

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

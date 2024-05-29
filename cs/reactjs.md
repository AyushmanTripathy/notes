# React JS

### State

- state is like memory of each component
- state should be owned by a common parent

### Immutability

- states should not be mutated in react
- reason:

```js
x = 100;
//next render will override the prev x value
setX(0); 
```

- also, setting to same reference that is modified doesn't work
- because react considers them same and hence no rerender
- local mutations are fine, mutating object before setting it as state

### Queueing of state updates

- state changes after a completing a re-render
- hence value of x will change only by one

```js
setX(x + 1);
setX(x + 1);
```

- instead changes can be queued
- gives correct result

```js
setX(x => x + 1);
setX(x => x + 1);
```

### Minor things

- returing null for not rendering anything
- render if true with `&&` (NOTE: dont use numbers as condition)

```js
<p> ayushman {doLastName && "tripathy"} </p>
```

- remember, if condition is 0, react will render 0

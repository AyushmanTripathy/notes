# Svelte 5

from: [Svelte Docs](https://svelte.dev/docs/svelte/overview)

### Event Delegation

- to reduce memory usage, handler are runned by application root
- hence avoid `e.stopPropagation()`
- manually dispatching events needs `{ bubbles: true }`
- using `on` from `svelte/events` is preperable

# Runes

## $state

- this is deeply reactive, hence updating will also trigger updates
- These objects are proxies hence they are not actaully mutated

### $state.raw

- not deeply reactive, hence better performance
- has to be reassigned
- can contain other $state() elements

### $state.snapshot

- takes the static snapshot
- is not a proxy
- used when providing data to external libraries

### passing $state to functions

- js is a pass by value language

```js
const double = (getA) => {
    return () => getA() * 2;
};

let a = 10;
const doubled = double(() => a);
console.log(doubled()); //20
a = 20;
console.log(doubled()); //40
```

- passing state to functions behaves similarly

## $derived

- $derived expression should be free of side effect
- $state changes are disallowed inside $derived

1. $derived.by

- for more complicated expression, we can pass a function
- `$derived(expr)` is same as `$derived.by(() => expr)`

### Push Pull Reactivity

- notifying of the change, push
- read the value of state, pull
- $derived are reevaluated when they are pulled

## $effect

- not recommended to update state

### Not to synchronise state in $effect

because this can cause reading and writing the same state, leading to infinite loops

- use callbacks when ever possible
- writeable $derived can be acheived with get/set
- use `untrack` to mark state as not dependencies in $effect & $derived

```svelte
// not rerunned when time updates
$effect(() => {
	save(data, untrack(() => time);
})
```

## $props

- used to pass arguments to the component
- props can be reassigned, but should not be mutate unless specified as $bindable
- $state can be passed as props, mutating them will give `ownership_invalid_mutation` warning
- mutating props is a bad idea, using callbacks are preferable

### $props.id()

- gives an unique id for component instance
- used to id, for attributes

## $bindable

- props go one way, parent to child
- bindable should be used sparingly, to update state from child to parent

```svelte
<Child bind:key={valueInParent} />
```

- if parent does not provides this bind:key, default value can be specified

```svelte
let { key = $bindable("fallback") } = $props();
```

## $inspect

- used to console.log reactivly
- this is deeply reactive
- custom function instead of console.log can be used

```svelte
$inspect(value).with(custom)
```

### $inspect.trace()

- can be used inside of $effect and $derived
- prints which state changes triggered them
- can optionally take a label as first argument

## $host()

- allows access to parent element, when doing custom elements
- example for dispatching events

```svelte
// Child.svelte
<svelte:options customElement="my-child" />
```

```svelte
// Parent.svelte
<my-child></my-child>
```

## Markup

- following snippets are same

```svelte
<Child {attr} />
<Child attr={attr} />
```

```svelte
<Child {...obj} />
<Child name={obj.name} />
```

## each block

- each block loop over anything with length property
- as part is optional
- `{:else}` block when no elements are present
- example, display items in the array 3 times.

```svelte
{#each array as item, i}
	{#each { length: 3 }, j}
		{item}
	{/each}
{:else}
	No items in the array!
{/else}
```

## key block

- destroys and recreates a block when an expression changes
- can be used for css styles properties and etc.

```svelte
{#key expression}
	<h1 style=""> Hello </h1>
{/key}
```

## await block

- allows to branch for all possible states of Promise
- for SSR, only pending state will be rendered
- if expression is not a Promise, then block is rendered

```svelte
{#await expression}
	Waiting ...
{:then value}
	Here is {value}
{:catch}
	Oops!!
{/await}
```

- if pending state is not required, it can be omitted
- similarly for catch

```svelte
{#await expression then value}
	Here is {value}
{/await}
```

## snippet block

- used for eliminating duplicate markups
- no avaliable outside their scopes
- they can be recursive
- they can be passed to components as props
- any content inside the component tags, except for other snippets, becomes the children snippet
- they are just values, hence can be used in if blocks

```svelte
{#snippet heading(name)}
	<h1> heading for {name} </h1>
{/snippet}
```

## render tag

- can have js expression, ternary operator etc.

```svelte
{@render heading("Thomas Shelby")}
```

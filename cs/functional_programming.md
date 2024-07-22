# Functional Programming

Imperative: how
Declarative: what

## Closure

function bundled together with its lexical enviroment

```js
funciton greator(str) {
    return (name) => name + str
}

x = greator("hello")
console.log(x("ayush")) // hello ayush
```

here greator creates a closure

## Functor

A Functor is a type that supports the map operation (and some mathmatical properties).
Its a superset of Monads

## Monads

-   is a design pattern
-   lets you chain operations, while it manages the secret work
-   reduces boilerplate and abstracts away control flow and side effects

A monad is type that supports unit and bind operations (and some mathmatical properties).
bind operation is like `flatMap` and unit is like `wrap` function.

#### Wrapped Type

1. also called a monadic type
1. here wrapper type or the monad is `M<T>`
1. example `Array<T>` or `Promise<T>`

#### Unit function

1. also called return, pure, wrap
1. type signature, `T -> M<T>`
1. notice input and output have same type
1. example

```js
// Array
const unit = (x) => [x];
// Promise
const unit = (x) => Promise((res, rej) => res(x));
```

#### Transform function

1. a function that takes unwrapped type and returns a wrapped type
1. type signature is `T -> M<U>`
1. example type signature, `number -> Array<string>`
1. T and U denote that types can be different like above number and string

```js
// Array
const transform = (x) => [x * 2];
// Promise
const transform = (x) => new Promise((res, rej) => res(x * 2));
const transform = async (x) => x * 2;
```

#### Bind function

1. also known as `>>=`
1. understand as the `run` function
1. type signature is `M<T> -> (T -> M<U>) -> M<U>`
1. takes 2 args, a wrapped type and a transform function
1. returns a wrapped type
1. example

```js
// Array
arr.flatMap((x) => [x * 2]); //[2] -> [4]
// Promise
promise.then((x) => x * 2);
```

**NOTE** as async await is syntactic sugar for then, do is syntactic sugar for all bind functions

#### Example of Monads

1. Option / Maybe, represents possible non existance of value
1. Writer, accumulation of log data
1. Future / Promise, represents possiblility of currently not avaliable value
1. List, represents branching computations

Promise are technically not monads as they don't satisfy mathmatical properties.

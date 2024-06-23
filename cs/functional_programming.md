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

## Monads



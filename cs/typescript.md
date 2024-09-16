# Typescript

## Generics

```ts
function select<T extends Element = HTMLElement>(query: string): T {
  return document.querySelector<T>(query);
}
```

## Mics

- bar argument is not required to pass

```ts
function foo(bar?: type) {
}
```

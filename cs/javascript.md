# Weird Javascript things

1. NaN === NaN is false, use Number.isNaN
1. window.innerWidth is invalid for inspect mode mobile, use window.screen.width

## Quirks

### non-null assertion operato

Removes nullable values from type

```ts
const x: string | null
const y = x!
typeof y // string
```

### function with 'never' return

function with 'never' return type, tells typescript that further branching
is not possible generally meaning a exception will be throw

```ts
function throwError(): never {
    throw Error()
}

const user: User | null
if (!user)
    throwError()
typeof user // User
```

# Angular

## RxJS

- `Observable` -> `Pipe (operators)` -> `Observer`
- overview of https://rxjs.dev/guide/operators


- `Observable` - producer of data
- `Observer` - consumer of data
    - `next()`, `error()`, `complete()`
    - `error()` method catches `throw new Error("foobar")` and by default, **completes** the pipe
- `Pipe` - transformation of data
- connecting the pipe:
    - `observable.pipe(operator1(), operator2(), ...).subscribe(observer)`  

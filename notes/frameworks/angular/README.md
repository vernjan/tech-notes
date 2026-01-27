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

## Directives

- enhancements for elements
- unlike components, directives have no templates
- **attribute directives** - change the appearance or behavior of an element
    - `ngModel`
- **structural directives** - change the structure of the DOM
    - starts with `*`
    - `*ngIf`, `*ngFor`, `*ngSwitch`
    - in moderna Angular, all built-in structural directives can be replaced with template attributes `@if`, `@for`, `@switch`

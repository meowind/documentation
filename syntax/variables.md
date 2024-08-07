## Declaration
structure: `let [mut] <name>[: <type>] [= <expr>]`

examples:
1. storing immutable data
```
let data: int = 50;
```
variable type can be inferred
```
let data = 50;
```
2. mutating variable
```
let mut counter = 0;
counter += 1;
```
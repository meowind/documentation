
## Declared Functions
*(item)*

structure: `func <name>([<arg>, ...]) [-> <type> | let <name>: <type>] $INSIDE_OF_DETAIL ? [<block>] : <block>`\
modifiers: `pub`

### Examples:
1. entrypoint of program
```
func main() {
    console::write_ln("Hello world!");
}
```
2. join two string with whitespace and print to console
```
func concat_and_print(a: str, b: str) {
    console::write_ln("${a} ${b}");
}
```
3. double passed value and return result
```
func double(x: int) -> int {
    return x + x;
}
```
return type can be inferred
```
func double(x: int) {
    return x + x;
}
```
4. return variable syntax
```
// useful when working with arrays
func filter(input: int[], value: int) -> let output: int[] {
    for el in input {
        if el == value => output.push_end(el);
    }
}
```
## Anonymous Functions
*(expression)*

structure: `func([<arg>, ...]) [-> <type> | let <name>: <type>] <block>`

### Examples:
1. anonymous function in variable
```
func main() {
    let is_even = func(x: int) -> bool {
        return x % 2 == 0;
    }

    console::write_ln(is_even(5));
}
```
2. anonymous function as an argument
```
func main() {
    console::write_ln(filter([1, 2, 3, 4, 5], func(x: int) -> bool {
        return x % 2 == 0;
    }));
}

func filter(array: int[], condition: func(int) -> bool) -> let output: int[] {
    for el in array {
        if condition(el) => output.push(el);
    }
}
```
we can simplify filter() call with type inference
```
func main() {
    console::write_ln(filter([1, 2, 3, 4, 5], func(x) {
        return x % 2 == 0;
    }));
}
```
we can simplify filter() call even more with inline body
```
func main() {
    console::write_ln(filter([1, 2, 3, 4, 5], func(x) => return x % 2 == 0));
}
```
we can also pass variable that contains function or declared function
```
func main() {
    let is_even = func(x: int) -> bool {
        return !is_odd(x);
    }

    console::write_ln(filter([1, 2, 3, 4, 5], is_even));
    console::write_ln(filter([1, 2, 3, 4, 5], is_odd));
}

func is_odd(x: int) -> bool {
    return x % 2 != 0;
}
```

## Arguments
*(argument)*

structure: `<name>(: <type>) | ([: <type>] = <expr>)`

### Examples:
1. argument without default value (required)
```
func example(required_arg: int);
```
2. argument with default value (optional)
```
func example(optional_arg: int = 50);
```
type in optional arguments can be inferred
```
func example(optional_arg = 50);
```
## Calls
*(expression)*

structure: `<name>([<expr>, ...])`

### Examples:
1. call function without arguments
```
func example();

example();
```
2. call function with arguments
```
func example(a: int, b: str, c: bool);

example(5, "string", true);
```
3. call function with arguments using named arguments
```
func example(a: int, b: str, c: bool);

example(a: 5, b: "string", c: true);

// order does not matter
example(c: true, a: 5, b: "string");

// this is also possible
example(c: true, 5, "string");
```
named arguments could be helpful when calling function with many optional arguments
```
func example(a = 5, b = "string", c = true);

example(a: 60);
example(b: "other string");
example(c: false);
example(a: 100, b: "aaa");
```

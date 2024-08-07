## Declaration
structure: `func <name>([<arg>, ...]) [-> <type> | let <name>: <type>] <block>`\
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
## Arguments
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
type on optional arguments can be inferred
```
func example(optional_arg = 50);
```
## Calling
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
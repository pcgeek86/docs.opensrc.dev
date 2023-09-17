---
title: "Rust by Example: Writing Functions"
---

# Rust by Example: Writing Functions

In this article, we'll learn how to write simple functions in Rust.
For starters, you'll use the `fn` keyword to indicate the start of a new function declaration.

After you write some code, make sure that you **save your code** and the execute `cargo run` from the terminal.
Make sure that your terminal is in your project directory (containing the `Cargo.toml` file) when you run this command!
If you open a new shell, you'll need to navigate back to your project directory before executing `cargo run`.

## Create New Rust Project

As with any Rust project, create a new project using `cargo new test-function` and then change into that directory with `cd test-function`.

## Write Your First Rust Function

Rust functions are simple to define. Simply use the `fn` keyword, then specify a function name, followed by parentheses, and curly brackets.

The parenthese denote any input arguments. You can either have no input arguments, with empty parentheses, or define as many as you'd like.

The curly braces denote your Rust function's body. This is the code that will be executed when you call (aka. invoke) your Rust function from somewhere else in your program.

```rust
fn do_something() {
}
```

Right now, this function doesn't do anything, so let's add some "work" inside the function's body.

```rust
fn do_something() {
  println!("Hello from Rust!");
}
```

In this updated function, we added a call to the built-in `println!` Rust macro.
This macro simply prints some information to the standard output of your terminal.

## Call Your Rust Function

If you'd like to call (invoke) your Rust function from your main() function entrypoint, simply use the example code below.

```rust
fn main() {
  do_something();
}
```

Later on, we'll see how you can call Rust functions with input arguments.
This example shows how to call your Rust function without any input arguments.

## Function Scoped Variables

You can define variables within a Rust function. These variables will go out of scope when the function scope ends, and their values will be dropped from memory.
Use the `let` keyword to indicate that you are declaring a new variable.

```rust
fn do_something() {
  let first_name = "Trevor";
  println!("Hello {first_name}!");
}
```

If you try to use the `first_name` variable from your main function, you will receive an error, because the variable is declared within the `do_something()` function scope.
After the `do_something()` function scope ends, the `first_name` variable is dropped, and cannot be used elsewhere in your program.

Also notice that we can reference variables in the `println!` macro, by surrounding the variable name in curly braces.
You cannot use arbitrary Rust expressions in this manner, as with some other languages, but you can reference variables.

## Input Arguments

Let's take a look at an example of declaring a Rust function with input arguments.

```rust
fn do_something(first_name: &str) {
  println!("Hello {first_name}!");
}
```

This function decalaration defines a single input argument called `first_name`, and the data type of this argument is `&str` (static string slice).
We can invoke this function by specifying a value that matches the data type defined by the argument.

:::note Named Arguments Not Supported by Rust
Rust does not support the concept of "named arguments." This refers to a syntax where the argument name can be specified directly before the value that's being passed into that argument.
Named arguments can allow the order of input arguments to be ignored, but again, Rust does not currently support this.
:::

Let's go ahead and call our custom function from `main()`.

```rust
fn main() {
  do_something("Trevor");
}
```

As you can see, we are specifying a `&str` value by specifying it in double quotes.

Rust supports another string type called `String`, which is heap-allocated. Don't worry about heap allocation, if you don't understand it, for now.
The `String` type is a bit more flexible and can store values of different sizes.
Let's re-define our function to use the `String` type instead.

```rust
fn do_something(first_name: String) {
  println!("Hello {first_name}!");
}
```

Even though we changed the data type of the input argument, we can still embed the value in our call to the `println!` macro.
This is possible because `String` implements a standard trait called `Display`, as you can [see in the Rust documentation](https://doc.rust-lang.org/std/string/struct.String.html#impl-Display-for-String).

When we invoke our updated function from `main()`, we must specify a `String` value as input, rather than `&str`.
You can use the `.to_string()` function to perform this conversion.

```rust
fn main() {
  do_something("Trevor".to_string());
}
```

## Multiple Input Arguments

Rust functions also support multiple input arguments.
Let's say that we want to pass a person's first name, as well as their age as input to a function.
An unsigned 8-bit integer can hold any value from 0 through 255.
That would be a suitable data type to use for an `age` parameter.
In order to define an unsigned 8-bit integer in Rust, we use `u8` as the data type.

```rust
fn do_something(first_name: String, age: u8) {
  println!("Hello {first_name}! Your age is {age}.");
}
```

Now that we have declared two input arguments, we can call this function from `main()`.

```rust
fn main() {
  do_something("Trevor".to_string(), 29);
}
```

Because the Rust compiler knows that the `do_something()` function accepts a `u8` as its second input argument for `age`, we don't need to specify the data type.
However, if you prefer to be explicit with your input data types, you can use the following Rust syntax.

```rust
fn main() {
  do_something("Trevor".to_string(), 29u8);
}
```

Although this syntax may look a bit odd, the `29u8` means "*represent the value 29 as an unsigned 8-bit integer*."
You can replace `u8` with any other data type that supports the same integer value, such as `u16`, `u128`, or even `i8` or `i64`.
You can read more about Rust integer types in the [official documentation](https://doc.rust-lang.org/book/ch03-02-data-types.html).

## Function Return Types

Rust functions can return values as well.
So far, our `do_something()` function has only accepted input arguments, because it does not define a return type.
Let's start by adding a return type declaration to the function.

```rust
fn do_something(first_name: String, age: u8) -> String {
  return format!("Hello, {first_name}! Your age is {age}.");
}
```

This function declaration accepts the same input arguments as the last section, but also indicates that it returns a `String` value.
We've changed the function body to use the `return` keyword, which tells Rust that our function is returning a value from the following expression.
Instead of using the `println!` macro this time, we're using the `format!` macro, which returns a String value, instead of writing it directly to the terminal.

Now, let's call this function from our `main()` function.

```rust
fn main() {
  do_something("Trevor".to_string(), 29u8);
}
```

If you run this program with `cargo run`, you won't see any output.
That's because the function call returns a String, but we're not actually doing anything with it!
Let's capture the return value and print it to the terminal from `main()`.

```rust
fn main() {
  let result = do_something("Trevor".to_string(), 29u8);
  println!("{result}");
}
```

This time, we declare a new variable in our `main()` function scope, and capture the result from our function call.
Then, we use the `println!` macro in `main()` to write the resulting value to the terminal.

## Conclusion

If you've made it this far, you've written your first Rust function!
There's still a lot more to learn though.
Feel free to implement your own custom Rust functions, and use different input argument names and data types!

If you receive any error messages while you're writing code, make sure to research them and learn how to fix them.
Even though receiving error messages can be disheartening, as a developer, errors are actually your friends!
Errors are simply providing guidance that something is wrong, and the Rust compiler does a great job at guiding you on how to fix those issues.
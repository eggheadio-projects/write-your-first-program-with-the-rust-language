# Handle errors with unwrap() in Rust

[Video link](https://egghead.io/lessons/rust-handle-errors-with-unwrap-in-rust)

Let's say we have a simple function that will sum two numbers. In our function signature, we will specify the type of each of the incoming variables, as well as the return type.

```rs
fn sum(a: u32, b: u32) -> u32 {
    a + b
}
```

We can then prompt our user to give us the two numbers.

```rs
use std::io;

fn main() {
    println!("Please enter a first number: ");

    let mut first = String::new();
    io::stdin().read_line(&mut first);

    println!("Please enter a second number: ");

    let mut second = String::new();
    io::stdin().read_line(&mut second);

}

fn sum(a: u32, b: u32) -> u32 {
    a + b;
}
```

Each of these variables are of type string which we can't pass to the sum function as it expects numbers. If we try to run this program we will get an error explaining this.

```shell
14 | let result = sum(first, second);
   |    ---                  ^^^^^^ expected u32, found struct `std::string::String`
```

To fix this we'll need a new variable, `a`, of type `u32`. We will first trim the input to make sure that there are no carriage returns or new lines. Then, we will call a method `parse()` which tries to parse the string into a number. We will do this for both value.

```rs
...

  let a:u32 = first.trim().parse();
...
  let b:u32 = second.trim().parse();
...
```

When we run this, we get a new error (sometimes developing can be seen as successful if we get a new error :)).

```shell
 --> src/main.rs:8:17
  |
8 |     let a:u32 = first.trim().parse();
  |                 ^^^^^^^^^^^^^^^^^^^^ expected u32, found enum `std::result::Result`
  |
  = note: expected type `u32`
             found type `std::result::Result<_, _>`
```

Our compiler was expecting `a` to be `u32` but it is actually a `Result` type. This is a wrapper that either resolves as a value or an error.

The easiest way to get at that value is to call the `::unwrap()` method. Let's see what happens when we do that.

```rs
fn main() {
    println!("Please enter a first number: ");

    let mut first = String::new();
    io::stdin().read_line(&mut first);
    let a:u32 = first.trim().parse().unwrap();

    println!("Please enter a second number: ");

    let mut second = String::new();
    io::stdin().read_line(&mut second);
    let b:u32 = second.trim().parse().unwrap();

    let result = sum(a,b);
    println!("{} + {} = {}", a,b, result);
}

fn sum(a: u32, b: u32) -> u32 {
  a + b
}
```

This time our program works - it will let us enter in numbers and calculate their sum:

```shell
Please enter a first number:
5
Please enter a second number:
3
5 + 3 = 8
```

However, before that happens it gives us a warning:

```shell
   |
13 |     io::stdin().read_line(&mut second);
   |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   |
   = note: this `Result` may be an `Err` variant, which should be handled
```

If we enter something that is not a number, we will make our program panic (poor program).

```shell
Please enter a first number:
hello
thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: ParseIntError { kind: InvalidDigit }', src/libcore/result.rs:1165:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.
```

We can see the error is of type `ParseIntError`. Note, the `unwrap()` method should only be used for quick development and not for production code.

## Personal take

Moving to compiler code is a really interesting transition. Working through each of the issues at compile time can allow more confidence that at run time our code is more resilient and secure. I wonder where testing fits in?

In this case, handling errors with unwrap() seems to mean panic if you get an error, otherwise keep going.

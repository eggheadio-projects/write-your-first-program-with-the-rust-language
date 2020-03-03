# Handle errors in Rust using Pattern Matching

[Video link](https://egghead.io/lessons/egghead-handle-errors-in-rust-using-pattern-matching)

The best approach to error handling here is to use Rust's build in pattern matching.

Here we first declare our mutable value `a`. Then, we use the `match` keyword along with the expression that can return a `Result` type.

In our case, this is `first.trim().parse().

In the `Ok` case, we have access to the value and we can simply assign that to the variable.

in the `Err` case, we just want to print a message. Since we are not going to use the passed error object, we prefix it with an `_`.

```rs
use std::io;

fn main() {
    println!("Please enter a first number: ");

    let mut first = String::new();
    io::stdin().read_line(&mut first).unwrap();

    let mut a:u32 = 0;
    match first.trim().parse() {
        Ok(val) => a = val,
        Err(_err) => {
            println!("Not a valid number!");
        }
    };
        ....
```

If we follow those same steps for our second number, the program now looks like this:

```rs
use std::io;

fn main() {
    println!("Please enter a first number: ");

    let mut first = String::new();
    io::stdin().read_line(&mut first).unwrap();

    let mut a:u32 = 0;
    match first.trim().parse() {
        Ok(val) => a = val,
        Err(_err) => {
            println!("Not a valid number!");
        }
    };

    println!("Please enter a second number: ");

    let mut second = String::new();
    io::stdin().read_line(&mut second).unwrap();

    let mut b:u32 = 0;
    match first.trim().parse() {
        Ok(val) => b = val,
        Err(_err) => {
            println!("Not a valid number!");
        }
    };

    let result = sum(a, b);
    println!("{} + {} = {}", a, b, result);
}

fn sum(a: u32, b: u32) -> u32 {
    a + b
}

```

Now, when we run the program and don't pass a number, we no longer get the stack trace but do see our error message.

```shell
Please enter a first number:
sadf
Not a valid number!
Please enter a second number:
```

## Personal take

Feel like I understand the `match` case and how it is better than the other methods so far.

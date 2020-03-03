# Handle errors in Rust using expect()

[Video link](https://egghead.io/lessons/rust-handle-errors-in-rust-using-expect)

A slightly better way to unwrap a result type is to use the expect method as opposed to unwrap. Expect gives us the opportunity to pass a message to the user, such as "This is not a valid number," which is a bit more useful than what unwrap returns.

```rs
use std::io;

fn main() {
    println!("Please enter a first number: ");

    let mut first = String::new();
    io::stdin().read_line(&mut first).unwrap();
    let a:u32 = first.trim().parse().expect("This is not a valid number");

    println!("Please enter a second number: ");

    let mut second = String::new();
    io::stdin().read_line(&mut second).unwrap();
    let b:u32 = first.trim().parse().expect("This is not a valid number");

    let result = sum(a, b);
    println!("{} + {} = {}", a, b, result);
}

fn sum(a: u32, b: u32) -> u32 {
    a + b
}
```

If we now run the program and enter an invalid value, we'll see the error message shows up in this text trace.

```shell
Please enter a first number:
ds
thread 'main' panicked at 'This is not a valid number.: ParseIntError { kind: InvalidDigit }', src/libcore/result.rs:1165:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace.
```

## Personal take

So, we still panic but now we are able to give more guidance to our user.

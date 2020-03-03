# Read user input from stdin in Rust

[Video link](https://egghead.io/lessons/rust-read-user-input-from-stdin-in-rust)

Reading user input from stdin can be done by importing the io module from Rust standard library.

```rs
use std::io;
```

We then create an instance of stdin using the stdin() function. This comes with a method read_line. Read_line takes a mutable reference to a string buffer.

```rs
fn main() {
  println!("Please enter your name: ");
  io::stdin().read_line();
}
```

Let's create a mutable variable name which is a string and pass a reference to that to read_line.

```rs
fn main() {
  println!("Please enter your name: ");
  let mut name = String::new();
  io::stdin().read_line(&mut name);
}
```

The reason read_line takes a mutable reference to a string buffer is because it will use this buffer to fill in the data that is entered by the user.

After the user is done entering their data, we can output the data using println!

```rs
fn main() {
  println!("Please enter your name: ");
  let mut name = String::new();
  io::stdin().read_line(&mut name);
  println!("{}", name);
}
```

We save the file and run the code. We'll notice that the compiler warns us about the fact that read_line returns something of type result, which can possibly be an error. It also tells us that the error should be handled.

```shell
 --> src/main.rs:6:3
  |
6 |   io::stdin().read_line(&mut name);
  |   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: `#[warn(unused_must_use)]` on by default
  = note: this `Result` may be an `Err` variant, which should be handled
```

However, our program still functions.

## Personal take

I thought I'd be able to pass `read_line(&name)` as the value is mutable but we have to use `read_line(&mut name)` to show that the reference is mutable also. You can't have a mutable reference to an immutable object, but you can have an immutable reference to a mutable object. Sounds like a tongue twister.

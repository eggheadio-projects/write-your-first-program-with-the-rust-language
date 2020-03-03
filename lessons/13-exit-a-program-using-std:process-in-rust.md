# Exit a program using std::process in Rust

[Video lesson](https://egghead.io/lessons/egghead-exit-a-program-using-std-process-in-rust)

To exit a program, use the process module from Rust standard library, and then call process::exit, which will exit the program with an exit code.

```rs
use std::process;

fn main() {
  process::exit(0);
}
```

Any exit code that is not 0 means that the program has exited with an error.

Now, we can exit our program with an error.

```rs
use std::io;
use std::process;

fn main() {
    println!("Please enter a first number: ");

    let mut first = String::new();
    io::stdin().read_line(&mut first).unwrap();

    let a:u32;

    match first.trim().parse() {
        Ok(val) => a = val,
        Err(_err) => {
            println!("Not a valid number!");
            process::exit(1);
        }
    };

    println!("Please enter a second number: ");

    let mut second = String::new();
    io::stdin().read_line(&mut second).unwrap();

    let b:u32;

    match first.trim().parse() {
        Ok(val) => b = val,
        Err(_err) => {
            println!("Not a valid number!");
            process::exit(1);
        }
    };

    let result = sum(a, b);
    println!("{} + {} = {}", a, b, result);
}

fn sum(a: u32, b: u32) -> u32 {
    a + b
}
```

We also no longer need to make our a variable mutable and assign an initial value, because the program will either assign an initial value, in case parsing was successful, or in case of an error it will exit the program.

Now, if we have an invalid input the program exits with an error code and prints our error message.

```shell
Please enter a first number:
asdas
Not a valid number!
```

## Personal take

Great! Now I can exit the program. The standard library seems to have a lot of helpful functionality ready to go.

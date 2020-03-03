# Make your Rust code more DRY

[Video lesson](https://egghead.io/lessons/egghead-make-your-rust-code-more-dry)

Let's take this duplicated functionality of reading the input and parsing the value, and put it in a separate function.

For that, we go ahead and create a function, readUserInput(), which will return a number. Then, we just take one of our input functionalities, copy it over, and make it a little bit more generic. Last but not least, we need to return the digit.

```rs
fn read_user_input() -> u32 {
    let mut input = String::new();
    io::stdin().read_line(&mut input).unwrap();

    let digit:u32;

    match input.trim().parse() {
        Ok(val) => digit = val,
        Err(_err) => {
            println!("Not a valid number!");
            process::exit(1);
        }
    };

    digit
}
```

Then we can go ahead and make use of that function by saying, `let a = readUserInput()`. We can do exactly the same for our variable b.

```rs
use std::io;
use std::process;

fn main() {
    loop {
        println!("Please enter a first number: ");
        let a = read_user_input();

        println!("Please enter a second number: ");
        let b = read_user_input();

        let result = sum(a, b);
        println!("{} + {} = {}", a, b, result);
    }
}

fn sum(a: u32, b: u32) -> u32 {
    a + b
}

fn read_user_input() -> u32 {
    let mut input = String::new();
    io::stdin().read_line(&mut input).unwrap();

    let digit:u32;

    match input.trim().parse() {
        Ok(val) => digit = val,
        Err(_err) => {
            println!("Not a valid number!");
            process::exit(1);
        }
    };

    digit
}
```

It still works and still keeps us asking us for numbers. That's how you make your code a bit more dry.

## Personal take

Wow! A short course but so much in there. Really whet my appetite for more Rust Lang learning :)

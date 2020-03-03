# Write and call a function in Rust

[Video link](https://egghead.io/lessons/rust-write-and-call-a-function-in-rust)

Let's define a function, `say_name`, that will take the first and last name and print them to the screen.

In the function definition, we give the type of each of the variables that are passed through after a colon.

We can then use them as we used them in our previous `main` example.

```rs
fn say_name(first: String, last: String) {
    println!("{} {}", first, last);
}
```

We can then call this function within our main function. It is necessary to pass through variables of the correct type otherwise the program will not compile.

```rs
fn main() {
    let first = "Pascal".to_string();
    let last = "Precht".to_string();

    say_name(first, last);
}

fn say_name(first: String, last: String) {
    println!("{} {}", first, last);
}
```

## Personal take

The observant will notice the appearance of the `.to_string()` method at the end of each string. If you try to compile and run the program without this conversion you get this error:

```shell
5 |   say_name(first, last);
  |                   ^^^^
  |                   |
  |                   expected struct `std::string::String`, found &str
  |                   help: try using a conversion method: `last.to_string()`
  |
  = note: expected type `std::string::String`
             found type `&str`
```

Looking [here](https://doc.rust-lang.org/std/str/index.html) in the docs, we can see that `&str` is one of two string types, the other bring `String`. We declared our function took `String`, so we need to convert. `&str` is a string slice rather than a string.

Pascal discusses this in more detail [ogsn his blog here](https://blog.thoughtram.io/string-vs-str-in-rust/).

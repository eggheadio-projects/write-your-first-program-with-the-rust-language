# Variables and Mutability in Rust

[Video link](https://egghead.io/lessons/rust-variables-and-mutability-in-rust)

Variables in Rust are created using the let keyword. Let's create a variable name using let name = Pascal.

```rs
fn main() {
  let name = "Pascal";
}
```

To output this variable, we can use the println!() function. However, println!() takes a string as a parameter, but since name is not a string but a variable, we have to use the placeholder syntax, which is using curly braces. Then we can pass name as a second argument to this function.

```rs
fn main() {
  let name = "Pascal";
  println!("{}", name);
}
```

Rust will take the first argument, `name`, and replace the placeholder with the value.

We can save the program and run it - we'll see it prints the name.

```bash
cargo run
```

Output:

```bash
   Compiling say-my-name v0.1.0 (/Users/kevin/code/egghead-intro-to-rust-notes/exercise/say-my-name)
    Finished dev [unoptimized + debuginfo] target(s) in 0.93s
     Running `target/debug/say-my-name`
Pascal
```

In Rust, values are immutable by default. This means that if we try to assign a new value to our variable the program will not compile. Instead, we'll get a clear complaint about this.

```rs
fn main() {
  let name = "Pascal";
  println!("{}", name);
  name = "Alice";
  println!("{}", name);
}
```

Output

```shell
   Compiling say-my-name v0.1.0 (/Users/kevin/code/egghead-intro-to-rust-notes/exercise/say-my-name)
error[E0384]: cannot assign twice to immutable variable `name`
 --> src/main.rs:4:5
  |
2 |     let name = "Pascal";
  |         ----
  |         |
  |         first assignment to `name`
  |         help: make this binding mutable: `mut name`
3 |     println!("{}", name);
4 |     name = "Alice";
  |     ^^^^^^^^^^^^^^ cannot assign twice to immutable variable

error: aborting due to previous error

For more information about this error, try `rustc --explain E0384`.
error: could not compile `say-my-name`.

To learn more, run the command again with --verbose.
```

These error messages are normally really informative and can help point you in the right direction when debugging.

The compiler even tells us that the first assignment has happened to name in the second line of our program. It also tells us that we need to make the binding mutable using the `mut` keyword.

If we change the variable to a mutable variable using the mute keywords and we run the program again, we'll see that it's successfully compiled without any problems.

```rs
fn main() {
  let mut name = "Pascal";
  println!("{}", name);
  name = "Alice";
  println!("{}", name);
}
```

It might feel frustrating to define mutability every time you need it but because of this feature you can tell just by looking at the code whether a value could be changed. This is very useful in debugging.

## Personal take

Mutations and mutability are good concepts to be aware of and Rust handles them quite explicitly. I quite like that Rust plays it safe and declares all things to be immutable by default.

## Resources

[Variables and mutability](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html) from the Rust Lang book.

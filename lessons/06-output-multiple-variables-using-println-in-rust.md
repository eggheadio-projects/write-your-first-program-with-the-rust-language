# Output multiple variables using println!() in Rust

[Video link](https://egghead.io/lessons/rust-output-multiple-variables-using-println-in-rust)

To output multiple variables, println supports multiple placeholders as well. We use the placeholders in the target string and pass through the variables in the order we want them to be used.

```rs
fn main() {
  let name = "Pascal";
  let another_name = "Alice";

  println!("{} and {}", name, another_name);
}
```

When the code runs, Rust will replace the variables in order. This can be done with as many placeholders as required.

## Personal take

I'm used to this syntax with Python. Though, there you have the option to be more declarative with the placeholders and not just depend on order. I wonder if that's true for Rust? Apparently it is ([see here](https://doc.rust-lang.org/std/fmt/)).

Still loving the inline code editor!

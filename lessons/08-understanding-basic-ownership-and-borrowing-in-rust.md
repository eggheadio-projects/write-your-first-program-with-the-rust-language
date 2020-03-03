# Understanding basic Ownership and Borrowing in Rust

[Video link](https://egghead.io/lessons/egghead-understanding-basic-ownership-and-borrowing-in-rust)

Let's look at a basic function and function call. We declare `first_name` and then pass it to our function. Our function prints the string to the screen.

```rs
fn main() {
  let first_name = "Pascal".to_string();
  say_first_name(first_name);
}

fn say_first_name(first: String) {
  println!("{}", first)
}
```

This works as expected. However, if we call the function for a second time we'll see that the compiler complains.

```rs
fn main() {
  let first_name = "Pascal".to_string();
  say_first_name(first_name);
  say_first_name(first_name);
}

fn say_first_name(first: String) {
  println!("{}", first)
}
```

Output:

```shell
2 |   let first_name = "Pascal".to_string();
  |       ---------- move occurs because `first_name` has type `std::string::String`, which does not implement the `Copy` trait
3 |   say_first_name(first_name);
  |                  ---------- value moved here
4 |   say_first_name(first_name);
  |                  ^^^^^^^^^^ value used here after move
```

So, the value was moved in line 3 and then we tried to use it after it was moved. This is caused by the `Ownership` concepts baked into Rust. This helps us to write memory safe code.

In Rust, every variable owns its value and when we pass a variable to a function the ownership of that value moves to the function.

We can't use the `first_name` again because once it has been used the value will be dropped.

If we do need access to `first_name` after the function, we'll need to pass it by reference. We need to update both our passing of the value and our function signature, prepending our variable names with an `&`.

```rs
fn main() {
  let first_name = "Pascal".to_string();
  say_first_name(&first_name);
  say_first_name(&first_name);
}

fn say_first_name(first: &String) {
  println!("{}", first)
}
```

In this way, we are passing a reference to the value rather than the value itself. This is also called `borrowing` in Rust and is a key concept in the language.

## Personal take

Passing by reference feels familiar from PHP, though that is far from being a strict language and the receiving function wouldn't complain if it received the string by reference or directly.

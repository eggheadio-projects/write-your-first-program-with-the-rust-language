# Compile and run a Rust program from scratch

[Video link](https://egghead.io/lessons/rust-compile-and-run-a-rust-program-from-scratch)

We start by creating a file `main.rs` and create a function main() using the fn keywords. This is the function that will be run when we execute our program.

```rs
fn main() {

}
```

To output "Hello, World" we use println!, or print line, which takes a string. We give it "Hello, World." Then we save the file.

```rs
fn main() {
  println!("Hello World");
}
```

Next, we compile the program using the rustc compiler.

```bash
rustc main.rs
```

Once that is done, we'll see that there is a new file called main, which can be executed straight from the command line.

## Personal take

I'm loving these baby steps. The syntax makes sense from a C perspective and the inline code editor on the egghead page is ace!

# Compile and run a Rust program using Cargo

[Video link](https://egghead.io/lessons/egghead-compile-and-run-a-rust-program-using-cargo)

We can compile a Rust project using Cargo and its build commands.

```bash
cargo build

   Compiling say-my-name v0.1.0 (~/code/egghead-intro-to-rust-notes/exercise/say-my-name)
    Finished dev [unoptimized + debuginfo] target(s) in 1.12s
```

This will create a target directory in which we can find the executable of our program. From here, we can again run our program on the command line.

A more convenient way to compile and run our Rust program is to use Cargo's run command.

```bash
cargo run
```

This one will compile and execute the program in one go. Cargo also comes with a clean command to remove the generated target.

```bash
cargo clean
```

Once executed, we can see that the target directory has been removed from the project. Although, the `Cargo.lock` file remains.

## Personal take

I know what each of these commands do - I've got a clear idea of the tools I need. Ready to dive into some more code :)

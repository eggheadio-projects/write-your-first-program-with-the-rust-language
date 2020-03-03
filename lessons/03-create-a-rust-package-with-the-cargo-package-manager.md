# Create a Rust package with the Cargo package manager

[Video link](https://egghead.io/lessons/rust-create-a-rust-package-with-the-cargo-package-manager)

The most convenient way to create a new Rust project is by using the Cargo package manager and its new commands.

```shell
cargo new say-my-name
```

The new command takes the name of a project. Once we execute it, we'll see that it has generated a bunch of files including a Git repository, a src directory and a Cargo.toml file. Note, if you execute this command within an existing git repo, the .gitignore and .git repo will not be generated.

```
.
├── Cargo.toml
└── src
    └── main.rs
```

The `src` directory only includes a `main.rs` file. If we take a look at its contents, we'll see it has a simple main() function that outputs "Hello, world!"

```rs
fn main() {
    println!("Hello, world!");
}
```

The `Cargo.toml` file is a package file that specifies the name of the project, its version, the author's name and its email address and the edition or version of the Rust programming language. Additionally, we can specify other configuration values such as dependencies or dev-dependencies.

## Personal take

Great to have `cargo` to scaffold a beginning project well.

## Resources

TOML stands for Tom's Obvious, Minimal Language. More details [here](https://github.com/toml-lang/toml).

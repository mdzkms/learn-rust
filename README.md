# How to try Rust without installing Rust components

If unable to install Rust and necessary tools for development (e.g. blocked by proxy), follow the steps below before being able to compile and run Rust code.

## Step 1

Pull a Rust docker image

```shell
$ docker pull rust
```

## Step 2

Provide a Rust project with a minimum structure such as

```shell
├── Cargo.toml
└── src
    └── main.rs
```

With `Cargo.toml` containing at least

```toml
[package]
name = "PROJECT_NAME"
version = "PROJECT_VERSION"
authors = ["AUTHOR_NAME <AUTHOR_EMAIL>"]
```

## Step 3

Write some code in `main.rs`

```rust
fn main() {
    println!("Hello World!");
}
```

## Step 4

Compile the code in `dev` / `debug` mode using docker

```shell
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/PROJECT_NAME -w /usr/src/PROJECT_NAME rust cargo build
```

or compile it in `release` mode

```shell
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/PROJECT_NAMEt -w /usr/src/PROJECT_NAME rust cargo build --release
```

## Step 5

Run the compiled executable

```shell
$ ./target/debug/PROJECT_NAME
```

Or use the command below if compiled as `release`

```shell
$ ./target/release/PROJECT_NAME
```

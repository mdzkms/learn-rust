# How to Try Rust Without Installing Rust Components

If unable to install Rust and necessary tools for development (e.g. blocked by proxy), follow these step before being able to compile and run Rust code.

## Setup

Before continuing with either option, pull a Rust docker image first.

```bash
$ docker pull rust
```

You can work from scratch or use an existing project.

### Initialize a new project

Let `cargo` generate the new project directory and files.

```bash
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/grrs -w /usr/src/grrs rust cargo new PROJECT_NAME
```

### Work with existing code

Provide a Rust project with a minimum structure such as below.

```bash
├── Cargo.toml
└── src
    └── main.rs
```

With `Cargo.toml` contents as follows.

```toml
[package]
name = "PROJECT_NAME"
version = "PROJECT_VERSION"
```

## Development

### Step 1

Write some code in `main.rs`.

```rust
fn main() {
    println!("Hello World!");
}
```

### Step 2

To add dependencies, append an entry in `Cargo.toml` file.

```toml
[dependencies]
dependency-name = "DEPENDENCY_VERSION"
```

If `[dependencies]` is already declared no need to write it again, just add the dependency below the last entry.

### Step 3

To make Cargo update the `Cargo.lock` file and fetch the new dependencies, run this command.

```bash
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/PROJECT_NAME -w /usr/src/PROJECT_NAME rust cargo build
```

### Step 4

To make Cargo update dependencies to their latest version run this.

```
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/PROJECT_NAME -w /usr/src/PROJECT_NAME rust cargo update
```

### Step 5

Compile the code in `dev` / `debug` mode using docker.

```bash
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/PROJECT_NAME -w /usr/src/PROJECT_NAME rust cargo build
```

or compile it in `release` mode.

```bash
$ docker run --rm --user "$(id -u)":"$(id -g)" -v "$PWD":/usr/src/PROJECT_NAMEt -w /usr/src/PROJECT_NAME rust cargo build --release
```

### Step 6

Run the compiled executable.

```bash
$ ./target/debug/PROJECT_NAME
```

Or use the command below if compiled as `release`.

```bash
$ ./target/release/PROJECT_NAME
```

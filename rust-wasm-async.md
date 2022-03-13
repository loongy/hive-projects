# Rust + WASM + Async = <3

Asynchronous I/O is becoming common place. It has established itself as an efficient pattern for web applications. In fact, it is becoming the norm for any program that is doing any kind of non-trivial I/O (which is most programs). Rust is also becoming one of the go-to languages for writing programs that are being compiled to WASM (thanks to its mature WASM support).

However, all of the asynchronous runtimes in Rust either do not compile to WASM/WASI, or panic at runtime when compiled to WASM/WASI. This is because all of them use conditional variables, which are not supported in WASM. Having said that, there is nothing intrinsic about asynchronous runtimes that prevent them from working in WASM/WASI.

The objective of this project is to use Rust to write your own asynchronous runtime that works when compiled to WASM/WASI. This is an especially interesting task, because WASM/WASI does not have support for threads, so everything must be done on a single thread (e.g. in an event loop). For bonus points, use the `poll` API available in WASI to support file I/O. For even more bonus points, open a PR for `futures`, `tokio`, or `async-std`. Some helpful material:

- Futures: https://docs.rs/futures-preview/latest/futures/executor/index.html
- Tokio: https://tokio.rs
- Async-std: https://async.rs
- The Rust async book: https://rust-lang.github.io/async-book/
- Understanding futures: https://www.viget.com/articles/understanding-futures-in-rust-part-1/

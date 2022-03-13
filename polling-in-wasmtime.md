# Polling in Wasmtime

## Polling

When programs read and write to file descriptors (including sockets) the current thread blocks. This means that the thread is stuck waiting for the I/O operation to complete before it can do anything else. This is extremely inefficient.

In response to this, polling was created. In short, polling allows a thread to register its interest in doing an I/O operation, and then it receives a notification from the OS when such an operation is possible *without* blocking. This is a terribly simplified explanation of polling at best, but the important point is that polling is critical to doing efficient I/O operations, and it is rapidly becoming the norm. 

## Wasmtime

WASM programs are able to do polling, thanks to the `poll` function defined in the WASI standard. Wasmtime, a very popular WASM runtime, supports WASI. However, its implementation of `poll` is broken. This prevents the WASM community from moving forward with efficient implementations of I/O operations. This limitation is especially brutal given that WASM programs are single-threaded and cannot even take advantage of multi-threading as a way to mitigate blocking (i.e. non-polling) I/O operations.

## Project

The objective of this project is to create a Pull Request for Wasmtime that fixes its implementation of `poll`. Specifically, when using `poll` to write to a file descriptor, Wasmtime always immediately claims that the file descriptor is ready for writing (saying that zero bytes are ready to be written). Similarly, when using `poll` to read from a file descriptor, Wasmtime always immediately claims that the file descriptor is ready for reading (saying that one byte is ready to be read).

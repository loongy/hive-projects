# BLASM

The objective of this project is to make WASM suitable for machine learning and other applications that are heavily dependent on linear algebra.

## What is BLAS?

- What is BLAS: http://www.netlib.org/blas/
- An optimized and open-source implementation of BLAS: https://www.openblas.net

BLAS defines an API for vector and matrix operations. These kinds of operations form the foundations of machine learning libraries, linear algebra libraries, data processing libraries, and high-performance computing. Most programs that are dependent on number crunching use BLAS at some level.

## What is BLASM?

BLAS could be implemented directly in WASM. You *could* take the C implementation and compile it to WASM. However, this is not a good idea. There are fundamental performance limitations when using WASM that prevent a WASM implementation of BLAS from being suitable for high-performance computing. WASM does not run at native speeds, it cannot do multi-threading, it cannot access the GPU, it cannot access registers, it has limited SIMD instructions, and it cannot be directly optimized for the underlying hardware (by nature, WASM is meant to be hardware agnostic).

And so, this project proposes BLASM: a standard for how WASM runtimes should make BLAS functionality available to WASM programs. This is similar in concept to WASI (the WebAssmebly Systems Interface), but instead of making system calls available, the BLASM standard makes native BLAS implementations available. By making the BLAS API available to WASM programs (where the implementation is provided by the WASM runtime, and not written in WASM itself), BLASM will enable WASM programs to write highly efficient machine learning code, linear algebra libaries, and data processing libraries, something that is not currently possible.

## What is WASI

- What is WASI: https://wasi.dev
- WASI proposal template: https://github.com/WebAssembly/wasi-proposal-template

WASI is the WebAssembly System Interface. It is a standard that defines how WASM runtimes should make system calls available to WASM programs. However, in practice it has a fairly broad scope. It would be cool to open a WASI proposal that adds BLAS to the WASI standard. This would make BLAS available to all WASM programs that are running in a WASI-compliant runtime (which is most of them).

## Deliverables

- [ ] Write a [WITX](https://radu-matei.com/blog/wasm-api-witx/) template for BLAS routines.
- [ ] Fork [Wasmtime](https://wasmtime.dev) or [Wasmer](https://wasmer.io) and add the WITX template.
- [ ] Implement the WITX functions in [Wasmtime](https://wasmtime.dev) or [Wasmer](https://wasmer.io) using [OpenBLAS](https://www.openblas.net).
- [ ] Create a [WASI proposal](https://github.com/WebAssembly/wasi-proposal-template).


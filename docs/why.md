# Why pure Go

`go-ruby-zeitwerk/zeitwerk` reimplements Ruby's `zeitwerk` in **pure Go, with cgo disabled**. The slice of
Ruby it covers is **deterministic and interpreter-independent**: given its inputs,
the result is a pure function of those inputs — no live binding, no evaluation of
arbitrary Ruby. That is exactly the part that can — and should — live as a
standalone Go library, separate from the interpreter.

## Extracted for reuse, reusable by anyone

- any Go program can import `github.com/go-ruby-zeitwerk/zeitwerk` directly, with no Ruby runtime;
- the dependency runs the *other* way — `rbgo` binds this module as a native
  module for [go-embedded-ruby](https://github.com/go-embedded-ruby/ruby) (the same
  pattern as [go-ruby-yaml](https://github.com/go-ruby-yaml/yaml)), rather than
  this module depending on the interpreter;
- the behaviour is pinned by a **differential oracle** against reference Ruby,
  independent of any one consumer.

## Why pure Go matters here

Because the library is CGO-free, it:

- cross-compiles to every Go target with no C toolchain, and links into a single
  static binary;
- has **no dependency on the Ruby runtime** — the dependency runs the other way;
- can be differentially tested against the `ruby` binary wherever one is on
  `PATH`, while the cross-arch lanes still validate the library itself.

## WebAssembly

Because `zeitwerk` is pure Go with cgo disabled, it also compiles to **WebAssembly**
with no source changes and no C toolchain — so this slice of Ruby runs **in the
browser** and in server-side WASI runtimes:

```sh
# In the browser
GOOS=js GOARCH=wasm go build ./...

# WASI (wasmtime, wasmer, wazero, …)
GOOS=wasip1 GOARCH=wasm go build ./...
```

The same module that links into a native static binary therefore also ships as a
`.wasm` module, which is what lets `rbgo` and
[go-embedded-ruby](https://github.com/go-embedded-ruby/ruby) run this native
module inside a browser sandbox.

See [Reference](reference.md) for the import path and API.

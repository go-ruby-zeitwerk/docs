# Reference

The public API lives at the module root (`github.com/go-ruby-zeitwerk/zeitwerk`). It is
**Ruby-shaped but Go-idiomatic**: names mirror Ruby's `zeitwerk`, while the surface follows
Go conventions — value types, explicit errors, no global state.

## Install

```sh
go get github.com/go-ruby-zeitwerk/zeitwerk
```

## Import

```go
import "github.com/go-ruby-zeitwerk/zeitwerk"
```

## API reference

The authoritative, always-current API reference is generated from the source by
pkg.go.dev:

- **[pkg.go.dev/github.com/go-ruby-zeitwerk/zeitwerk](https://pkg.go.dev/github.com/go-ruby-zeitwerk/zeitwerk)**

The module's [README](https://github.com/go-ruby-zeitwerk/zeitwerk#readme) carries worked
examples and the full, up-to-date surface. This page intentionally links to those
canonical sources rather than duplicating signatures that could drift out of date.

## Conformance

Behaviour is pinned by a **differential oracle** against reference Ruby: a corpus
is run through both the `ruby` binary and this library and the results are compared,
gated on the reference where relevant and skipping itself where `ruby` is absent so
the cross-arch lanes still validate the library.

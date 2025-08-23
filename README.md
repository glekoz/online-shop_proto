# online-shop-proto

Shared Protocol Buffers (`.proto`) for the **online-shop** microservices.

This repository contains canonical protobuf definitions used across the `online-shop` microservice ecosystem (user, product, image, etc.). The goal is to maintain a single source of truth for message formats and service RPCs so each microservice can generate client/server code in its language of choice.

---

## Quickstart

### Prerequisites

* `protoc` (Protocol Buffers compiler) installed — v3.19+ recommended.
* `protoc-gen-go` and `protoc-gen-go-grpc` for Go code generation:

```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
```

### Generate Go code

From the repository root, run (example for all protos):

```bash
protoc \
  --proto_path=proto \
  --go_out=paths=source_relative \
  --go-grpc_out=paths=source_relative \
  proto/**/*.proto
```

## Importing protos in your services

* Add this repo as a git submodule, sub-tree, or fetch during CI so your build can reference `proto/` as an import path.
* Use `--proto_path` to include the `proto/` folder when running `protoc`.

Example (Go module service `go.mod`):

```bash
# in service repo
git submodule add https://github.com/glekoz/online-shop_proto proto
# generate code referencing the proto definitions
protoc --proto_path=proto --go_out=paths=source_relative:pkg/proto ...
```

---

## Contributing

Contributions are welcome. Keep changes minimal and add/update tests and examples when you change message semantics.

Preferred workflow:

1. Fork the repo
2. Create a branch `feat/your-change` or `fix/...`
3. Add or update `.proto` files and generated artifacts if required
4. Run `protoc` or `buf generate` locally and ensure no breaking changes, or explain why the change is breaking
5. Open a PR with a clear description and migration notes (if necessary)

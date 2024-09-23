# [`Substreams`](https://substreams.streamingfast.io/) for [**Cosmos**](https://cosmos.network/)

[<img alt="github" src="https://img.shields.io/badge/Github-substreams.cosmos-8da0cb?style=for-the-badge&logo=github" height="20">](https://github.com/pinax-network/substreams-cosmos)
[<img alt="crates.io" src="https://img.shields.io/crates/v/substreams-cosmos.svg?style=for-the-badge&color=fc8d62&logo=rust" height="20">](https://crates.io/crates/substreams-cosmos)
[<img alt="docs.rs" src="https://img.shields.io/badge/docs.rs-substreams.cosmos-66c2a5?style=for-the-badge&labelColor=555555&logo=docs.rs" height="20">](https://docs.rs/substreams-cosmos)
[<img alt="GitHub Workflow Status" src="https://img.shields.io/github/actions/workflow/status/pinax-network/substreams-cosmos/push.yml?branch=main&style=for-the-badge" height="20">](https://github.com/pinax-network/substreams-cosmos/actions?query=branch%3Amain)

> This library contains the generated Rust protobuf bindings for [Cosmos Block](https://buf.build/streamingfast/firehose-cosmos) as well as helper methods to extract and parse block data.

## 📖 Documentation

### <https://docs.rs/substreams-cosmos>

### Further resources

- [Substreams documentation](https://substreams.streamingfast.io)

## Install

```
cargo add substreams-cosmos
```

## Usage

Refer to [Docs.rs](https://docs.rs/substreams-cosmos/latest/substreams_cosmos/struct.Block.html#implementations) for helper methods on `Block` that extract action and transaction iterators from the Cosmos block.

**Cargo.toml**

```toml
[dependencies]
substreams = "0.5"
substreams-cosmos = "0.1"
```

**src/lib.rs**

```rust
use substreams::errors::Error;
use substreams_cosmos::pb::{Block, Events};

#[substreams::handlers::map]
fn map_events(block: Block) -> Result<Events, Error> {
    let mut events = vec![];

    for tx in block.tx_results {
        for event in tx.events {
            events.push(event);
        }
    }
    Ok(Events { events })
}
```

## Release

- Run `Make` if there were changes in protobufs
- Bump up version in workspace `Cargo.toml`
- Commit changes
- Tag a release: <https://github.com/pinax-network/substreams-cosmos/releases>
- Publish packages in this order: `core`, `substreams-cosmos`.

# NEAR Smart Contract Rust Template
### Modify for creating PR at ContractAid Github App workflow

Project structure for writing smart contracts for NEAR in Rust.

## Required Software

- [Rust & Cargo](https://www.rust-lang.org/tools/install)
  - With the WASM target installed: `rustup target add wasm32-unknown-unknown`
  - [cargo-make](https://crates.io/crates/cargo-make): `cargo install cargo-make`
- [Node.js](https://nodejs.org/)
  - The default initialization arguments script `args.sh` uses the Node.js interpreter, but that can easily be modified if you like. You probably will have Node.js installed anyways since it's required to use the NEAR CLI.
- [NEAR CLI](https://docs.near.org/tools/near-cli) ^3.4.1: `npm install -g near-cli`

## Usage

### Scripts

#### `cargo make clean`

Removes the `target` and `neardev` directories.

#### `cargo make test`

Runs unit tests using the default target. (Note: behavior may differ from simply running `cargo test` depending on the target specified in `.cargo/config.toml`.)

#### `cargo make build`

Compiles the smart contract to a WebAssembly binary. The binary path is `./target/wasm32-unknown-unknown/release/<package>.wasm`.

#### `cargo make call <method> <method-args> <...arguments>`

Calls the NEAR CLI:

```txt
near call <dev-account> <method> <method-args> <...arguments>
```

Where `<dev-account>` is the account ID of the most recent dev deployment on testnet.

#### `cargo make call-self <method> <method-args> <...arguments>`

Calls the NEAR CLI:

```txt
near call <dev-account> <method> <method-args> <...arguments> --accountId <dev-account>
```

Where `<dev-account>` is the account ID of the most recent dev deployment on testnet.

#### `cargo make view <method> <method-args> <...arguments>`

Calls the NEAR CLI:

```txt
near view <dev-account> <method> <method-args> <...arguments>
```

Where `<dev-account>` is the account ID of the most recent dev deployment on testnet.

#### `cargo make optimize`

Cleans up and optimizes the most recently-built WASM binary. The optimized binary path is `./deploy/<name>.wasm`.

**Note**: In order to optimize the WASM binary, you must have [`wasm-tools`](https://github.com/bytecodealliance/wasm-tools) installed:

```txt
cargo install wasm-tools
```

`wasm-tools` is also available on Homebrew:

```txt
brew install wasm-tools
```

#### `cargo make deploy <account-id>`

Deploys the most recently optimized WASM binary to `<account-id>` on the network specified by `NEAR_ENV`, and calls the `new` function with arguments generated by `args.sh`. (Implicitly calls `cargo make optimize` beforehand.)

#### `cargo make dev-deploy [--force]`

Deploys the most recently built WASM binary to the dev account in `neardev/`, or to a new dev account if `neardev/` is not found or `--force` is set. Calls the `new` function with arguments generated by `args.sh`.

## Authors

- Jacob Lindahl <jacob.lindahl@near.org> [@sudo_build](https://twitter.com/sudo_build)

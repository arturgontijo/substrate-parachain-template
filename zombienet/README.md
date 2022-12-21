# Setup

### Zombienet binary:

Download the binary from [Zombienet Releases](https://github.com/paritytech/zombienet/releases).

Copy it to `./bin`.

```shell
cd zombienet/

wget https://github.com/paritytech/zombienet/releases/download/v1.3.23/zombienet-linux-x64 -P ./bin
chmod +x ./bin/zombienet-linux-x64
# Or in MacOS:
wget https://github.com/paritytech/zombienet/releases/download/v1.3.23/zombienet-macos -P ./bin
chmod +x ./bin/zombienet-macos
```

Let’s make sure Zombienet CLI is installed correctly:
```shell
./bin/zombienet-linux-x64 --help
# Or in MacOS:
./bin/zombienet-macos --help
```

### Relay Chain Node Binary:

Download the binary from [Polkadot Releases](https://github.com/paritytech/polkadot/releases).

Copy it to `./bin`.

```shell
wget https://github.com/paritytech/polkadot/releases/download/v0.9.36/polkadot -P ./bin
chmod +x ./bin/polkadot

# Or in MacOS,
# generate it yourself from the code:

git clone -b release-v0.9.36 https://github.com/paritytech/polkadot
cd polkadot/
cargo build --release
cp ./target/release/polkadot ../bin/polkadot
```

### Parachain node Binary:

Build this repo and copy its binary node to `./bin`.

```shell
cd ..
cargo build --release
cp ./target/release/parachain-template-node zombienet/bin
cd zombienet
```

### Spawning the Network:

- Check your `./bin` content, it should have something like:

```shell
ls -shla ./bin
total 421M
4,0K drwxrwxr-x 2 . . 4,0K dec 21 19:10 .
4,0K drwxrwxr-x 3 . . 4,0K dec 21 19:06 ..
146M -rwxrwxr-x 1 . . 155M dec 21 19:10 parachain-template-node
114M -rwxrwxr-x 1 . . 116M dec 21 18:36 polkadot
162M -rwxrwxr-x 1 . . 162M dec 21 17:53 zombienet-linux-x64
```

- Run `zombienet` tool

```shell
./bin/zombienet-linux-x64 -p native spawn config.toml
# Or in MacOS:
./bin/zombienet-macos -p native spawn config.toml
```

- After `zombienet` boots up, open PolkadotJS UI in your browser:

[Relay Chain](https://polkadot.js.org/apps/?rpc=ws://127.0.0.1:9944#/explorer)

[Parachain Chain](https://polkadot.js.org/apps/?rpc=ws://127.0.0.1:9955#/explorer)

- Wait until your Parachain collator starts to produce blocks and check the `recent events` section.

---
id: run-node
title: Run a CKB Node
---

To get started on your journey with CKB, the first thing you can try is to run a CKB node yourself.

If you are not familiar with the concepts of node and mining yet, [here is a document](../basic-concepts/node-mining) you can learn from.

## Get CKB Client

To get the CKB client software, you can choose to download the released binary directly, or [build it from the source code](../dev-guide/compile), or [use docker](https://github.com/nervosnetwork/ckb/blob/develop/docs/run-ckb-with-docker.md).

> For Windows user, we recommend you to use Docker for running CKB node.

In this guidance we use the pre-built binary directly.

### Dependencies

For Linux user (not necessary for macOS user), you need to install `libssl` dynamic libraries before using the released binary.

```shell
sudo apt-get install -y libssl1.0.0
```

### Download

Download the binary file from the [CKB releases page on GitHub](https://github.com/nervosnetwork/ckb/releases):

<!-- Todo: change the release version here -->

<!--DOCUSAURUS_CODE_TABS-->

<!--macOS-->

```shell
wget https://github.com/nervosnetwork/ckb/releases/download/v0.12.0/ckb_v0.12.0_darwin_amd64.zip
```

<!--Linux-->

```shell
wget https://github.com/nervosnetwork/ckb/releases/download/v0.12.0/ckb_v0.12.0_linux_amd64.tar.gz
```

<!--END_DOCUSAURUS_CODE_TABS-->

> You can also find nightly build versions from the releases of the [ckb-builds repo](https://github.com/ckb-builds/ckb-builds/releases)

Then uncompress the file:

<!--DOCUSAURUS_CODE_TABS-->

<!--macOS-->

```shell
unzip ckb_v0.12.0_darwin_amd64.zip && \
cd ckb_v0.12.0_darwin_amd64
```

<!--Linux-->

```shell
tar -xzvf ckb_v0.12.0_linux_amd64.tar.gz && \
cd ckb_v0.12.0_linux_amd64
```

<!--END_DOCUSAURUS_CODE_TABS-->

After it is downloaded and unzipped, you need to copy the `ckb` binary file to a `PATH` directory. In the unzipped folder:

```shell
sudo ln -snf "$(pwd)/ckb" /usr/local/bin/ckb
```

Then check if it works with:

```shell
ckb --version
```

<!-- Todo: change the response here -->

<details>
<summary>(click here to view response)</summary>

```shell
$ ckb --version
ckb 0.12.0 (v0.12.0 2019-05-17)
```

</details>

If you see the response above, you have successfully installed CKB. You can try to [start a CKB node](#run-ckb) now.

## Run CKB

Here you will learn about how to start a CKB node.

### Configurations

You can generate the default configuration files for connecting with our testnet with the following command. It will make a workshop folder called `ckb-testnet` and the generated files will be in this folder:

```shell
ckb init -C ckb-testnet --spec testnet && \
cd ckb-testnet
```

<details>
<summary>(click here to view response)</summary>

```shell
$ ckb init -C ckb-testnet --spec testnet && \ 
cd ckb-testnet
Initialized CKB directory in /Users/username/code/ckb-testnet
export ckb.toml
export ckb-miner.toml
```

</details>

In `ckb.toml`, you will find the information of bootnodes. These nodes will serve as the seed nodes to help you discover other CKB nodes in the CKB network.

> On github there is document that talks about [how to configure CKB](https://github.com/nervosnetwork/ckb/blob/develop/docs/configure.md) in details.

### Start a Node

Now you can start the CKB client to run a node:

```shell
ckb run
```

<details>
<summary>(click here to view response)</summary>

```shell
$ ckb run
2019-05-18 08:06:37.246 +08:00 main INFO sentry  **Notice**: The ckb process will send stack trace to sentry on Rust panics. This is enabled by default before mainnet, which can be opted out by setting the option `dsn` to empty in the config file. The DSN is now https://48c6a88d92e246478e2d53b5917a887c@sentry.io/1422795
2019-05-18 08:06:37.257 +08:00 main INFO ckb_db::rocksdb  Initialize a new database
2019-05-18 08:06:37.385 +08:00 main INFO main  chain genesis hash: 0xaad9b82caa07f5989dfb8caa44927f0bab515a96ccaaceba82c7bea609fec205
2019-05-18 08:06:37.385 +08:00 main INFO network  Generate random key
2019-05-18 08:06:37.386 +08:00 main INFO network  write random secret key to "/Users/username/code/ckb-testnet/data/network/secret_key"
2019-05-18 08:06:37.391 +08:00 main INFO network  No peer in peer store, start seeding...
2019-05-18 08:06:37.392 +08:00 main INFO network  Listen on address: /ip4/0.0.0.0/tcp/8115/p2p/QmSbvRYNUujyEBEpRipdREfS8cqLxCSndDAWRDAE1Hms2H
2019-05-18 08:06:37.394 +08:00 tokio-runtime-worker-0 INFO network  p2p service event: ListenStarted { address: "/ip4/0.0.0.0/tcp/8115" }
2019-05-18 08:06:37.441 +08:00 tokio-runtime-worker-6 INFO network  SessionId(1) open, registry /ip4/47.111.169.36/tcp/8111/p2p/QmNQ4jky6uVqLDrPU7snqxARuNGWNLgSrTnssbRuy3ij2W success
```

</details>

Congratulations! You just started a CKB node!

If you find any error messages, don't worry, check out the [trouble shooting document](../references/troubleshooting).
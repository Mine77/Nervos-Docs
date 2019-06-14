---
id: run-node
title: 运行 CKB 节点
---

一旦你成功的 [创建了自己的钱包](wallet)，就可以开始试着运行节点了。

如果您还不熟悉节点和挖矿的概念，这里有一个 [您可以学习的文档](../basic-concepts/node-mining)。

## 获取 CKB 客户端

要获得CKB客户端软件，你可以选择直接下载官方发布的二进制文件，或者[从源代码编译获得可执行文件](../dev-guide/compile)或[使用 Docker](https://github.com/nervosnetwork/ckb/blob/develop/docs/run-ckb-with-docker.md) 来运行节点。

> 对于Windows用户，我们建议您使用 Docker 运行 CKB 节点。

在本教程中，我们将直接使用预先编译好的二进制可执行文件。

### 安装依赖软件

CentOS 用户请使用 `x86_64-unknown-centos-gnu` 软件包。另外还需要安装 OpenSSL 1.0 才能正常运行软件：

```shell
sudo yum install openssl-libs
```

### 下载软件

从 GitHub 上的 CKB 发布页面下载二进制文件：

<!-- Todo: change the release version here -->

<!--DOCUSAURUS_CODE_TABS-->

<!--macOS-->

```bash
curl -O -L https://github.com/nervosnetwork/ckb/releases/download/v0.13.0/ckb_v0.13.0_x86_64-apple-darwin.zip
curl -O -L https://github.com/nervosnetwork/ckb/releases/download/v0.13.0/ckb_v0.13.0_x86_64-apple-darwin.zip.asc
```

<!--Linux-->

```bash
wget https://github.com/nervosnetwork/ckb/releases/download/v0.13.0/ckb_v0.13.0_x86_64-unknown-linux-gnu.tar.gz
wget https://github.com/nervosnetwork/ckb/releases/download/v0.13.0/ckb_v0.13.0_x86_64-unknown-linux-gnu.tar.gz.asc
```

<!--CentOS-->

```bash
curl -L -O https://github.com/nervosnetwork/ckb/releases/download/v0.13.0/ckb_v0.13.0_x86_64-unknown-centos-gnu.tar.gz
curl -L -O https://github.com/nervosnetwork/ckb/releases/download/v0.13.0/ckb_v0.13.0_x86_64-unknown-centos-gnu.tar.gz.asc
```

<!--END_DOCUSAURUS_CODE_TABS-->

> 如果无法从命令行下载，您也可以 [直接从浏览器下载](https://github.com/nervosnetwork/ckb/releases/tag/v0.13.0) 。
> 
> `.asc` 文件是软件包的签名。 建议您亲自检查并确认文件的 [完整性](https://github.com/nervosnetwork/ckb/blob/develop/docs/integrity-check.md)。

然后解压缩文件：

<!--DOCUSAURUS_CODE_TABS-->

<!--macOS-->

```bash
unzip ckb_v0.13.0_x86_64-apple-darwin.zip && \
cd ckb_v0.13.0_x86_64-apple-darwin
```

<!--Linux-->

```bash
tar -xzvf ckb_v0.13.0_x86_64-unknown-linux-gnu.tar.gz && \
cd ckb_v0.13.0_x86_64-unknown-linux-gnu
```

<!--END_DOCUSAURUS_CODE_TABS-->

下载并解压缩后，需要将 `ckb` 二进制文件复制到 `PATH` 目录。 在解压缩的文件夹中：

```bash
sudo ln -snf "$(pwd)/ckb" /usr/local/bin/ckb
```

然后检查它是否正常工作：

```bash
ckb --version
```

<!-- Todo: change the response here -->

<details>
<summary>(点击此处查看响应)</summary>

```bash
$ ckb --version
ckb 0.13.0 (rylai-v2 v0.13.0 2019-06-01)
```

</details>

如果您看到上面的响应，则表示您已成功安装 CKB 软件。

## 配置

您可以使用以下命令生成用于连接我们的测试网所需要的默认配置文件。 它将创建一个名为 `ckb-testnet` 的文件夹，生成的配置文件将被放在此文件夹中：

```bash
ckb init -C ckb-testnet --chain testnet && \
cd ckb-testnet
```

<details>
<summary>(点击此处查看响应)</summary>

```bash
$ ckb init -C ckb-testnet --chain testnet && \
cd ckb-testnet
Initialized CKB directory in /Users/username/code/ckb-testnet
create ckb.toml
create ckb-miner.toml
```

</details>

然后，您可以在生成的 `ckb-testnet` 文件夹中找到 `ckb.toml` 文件，该文件夹包含CKB节点的配置。

要设置您的矿工钱包，您需要将 [钱包创建](wallet#create-wallet) 时获得的 `[block_assembler]` 添加到 `ckb.toml` 文件的末尾（请在以下命令中替换 `<YOUR-CODE_HASH>` 和 `<YOUR-ARGS>` 部分）

```bash
cat <<EOT >> ckb.toml
[block_assembler]
code_hash = "<YOUR-CODE_HASH>"
args = ["<YOUR-ARGS>"]
EOT
```

<details>
<summary>(点击此处查看响应)</summary>

```bash
$ cat <<EOT >> ckb.toml
[block_assembler]
code_hash = "0x9e3b3557f11b2b3532ce352bfe8017e9fd11d154c4c7f9b7aaaa1e621b539a08"
args = ["0x7e6bccda0abe748eb5dc74be0e797662ae938036"]
EOT
```

</details>

## 启动节点

现在您可以启动 CKB 客户端来运行节点：

```bash
ckb run
```

<details>
<summary>(点击此处查看响应)</summary>

```bash
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

恭喜！ 你刚刚启动了一个CKB节点！

如果您发现任何错误消息，请查看 [故障排除文档](../references/troubleshooting)。
---
id: wallet
title: 创建钱包
---

要开始使用 CKB，您首先需要为自己创建一个钱包。

我们提供了一个 [命令行工具CKB-CLI](https://github.com/TheWaWaR/ckb-cli) 来帮您完成这一步。

## 安装

从 [GitHub Release](https://github.com/TheWaWaR/ckb-cli/releases)下载最新版本的 CKB-CLI：

<!-- Todo: change the ckb-cli version here -->

<!--DOCUSAURUS_CODE_TABS-->

<!--macOS-->

```bash
curl -OL https://github.com/TheWaWaR/ckb-cli/releases/download/v0.1.2/ckb-cli-v0.1.2-apple-drawin.tar.gz
```

<!--macOS(中国镜像)-->

```bash
curl -O http://ckbbin.engpro.cryptape.com/ckb-cli-v0.1.2-apple-drawin.tar.gz
```

<!--Linux-->

```bash
wget https://github.com/TheWaWaR/ckb-cli/releases/download/v0.1.2/ckb-cli-v0.1.2-linux-musl.tar.gz
```

<!--Linux(中国镜像)-->

```bash
wget http://ckbbin.engpro.cryptape.com/ckb-cli-v0.1.2-linux-musl.tar.gz
```

<!--END_DOCUSAURUS_CODE_TABS-->

> 如果您发现下载文件很慢，您也可以选择直接</a>使用浏览器从网站下载 。</p> </blockquote> 
> 
> 然后解压缩文件并将其添加到系统路径：
> 
> <!--DOCUSAURUS_CODE_TABS-->
> 
> <!--macOS-->
> 
> ```bash
tar -xzvf ckb-cli-v0.1.2-apple-drawin.tar.gz && \
sudo ln -snf "$(pwd)/ckb-cli" /usr/local/bin/ckb-cli
```

<!--Linux-->

```bash
tar -xzvf ckb-cli-v0.1.2-linux-musl.tar.gz && \
sudo ln -snf "$(pwd)/ckb-cli" /usr/local/bin/ckb-cli
```

<!--END_DOCUSAURUS_CODE_TABS-->

现在您已成功安装了CKB-CLI。 您可以使用以下命令来检查它是否工作：

```bash
ckb-cli --version
```

<!-- Todo: change the response here -->

<details>
<summary>(点击此处查看响应)</summary>

```bash
$ ckb-cli --version
ckb-cli 0.1.2 ( 2019-05-29)
```

</details>

如果您看到上面的响应，则表示您已成功安装 CKB-CLI。

## 创建钱包

您可以使用以下命令来生成私钥：

```bash
ckb-cli wallet generate-key --privkey-path privkey
```

<details>
<summary>(点击此处查看响应)</summary>

```bash
$ ckb-cli wallet generate-key --privkey-path privkey
Put this config in < ckb.toml >:

[block_assembler]
code_hash = "0x9e3b3557f11b2b3532ce352bfe8017e9fd11d154c4c7f9b7aaaa1e621b539a08"
args = ["0x7e6bccda0abe748eb5dc74be0e797662ae938036"]

{
  "address": "ckt1q9gry5zg0e4ueks2he6gadwuwjlqu7tkv2hf8qpkf47x2u",
  "lock_hash": "0x66313b870633a267297b8e25ac56ec04b0c6153ca319f3a597816b6ba1c735a6",
  "pubkey": "02988df184fcc74a98e03d9952e878db068d31b5667c233985802ee4e7f3751323"
}
```

</details>

在输出消息中，您可以找到以下信息：

* 配置矿工软件需要`[block_assembler]` 部分 ，所以 **请务必记录下来**。
* `address` 是生成的[钱包的地址](../basic-concepts/states-tokens#wallet)。
* `lock_hash`是用来[解锁 Cell](../basic-concepts/architecture#lock-script) 用的。
* `pubkey` 是这个钱包的公钥。

此命令还将在当前文件夹中创建名为 `privkey` 的文件。 在此文件中，您可以找到您的私钥（文件的第一行）及其地址（第二行）。

<details>
<summary>（点击此处查看示例 <code>privkey</code>）</summary>

```bash
9404a426fa4a7b2e431f75e70d0b458233cbe04b8617935582cb39925892a429
ckt1q9gry5zg0e4ueks2he6gadwuwjlqu7tkv2hf8qpkf47x2u
```

</details>

> 请注意，您的私钥是使用您 Token 和资产的唯一钥匙。 丢失私钥或将其交给他人等价于失去您的 Token。

## 导入钱包

如果您已有私钥，则可以将其导入 CKB-CLI 以查看其地址或 `block_assembler` 信息。

您需要创建一个名为 `privkey` 的文件，其中包含您的私钥：

```bash
echo '<your-private-key>' > privkey
```

然后您可以看到您的钱包信息：

```bash
ckb-cli wallet key-info --privkey-path privkey
```

<details>
<summary>(点击此处查看响应)</summary>

```bash
$ echo '9404a426fa4a7b2e431f75e70d0b458233cbe04b8617935582cb39925892a429' > privkey
$ ckb-cli wallet key-info --privkey-path privkey
Put this config in < ckb.toml >:

[block_assembler]
code_hash = "0x9e3b3557f11b2b3532ce352bfe8017e9fd11d154c4c7f9b7aaaa1e621b539a08"
args = ["0x7e6bccda0abe748eb5dc74be0e797662ae938036"]

{
  "address": "ckt1q9gry5zg0e4ueks2he6gadwuwjlqu7tkv2hf8qpkf47x2u",
  "lock_hash": "0x66313b870633a267297b8e25ac56ec04b0c6153ca319f3a597816b6ba1c735a6",
  "pubkey": "02988df184fcc74a98e03d9952e878db068d31b5667c233985802ee4e7f3751323"
}
```

</details>

现在您已成功创建自己的钱包。 恭喜！ 您现在可以尝试启动自己的 CKB 节点了。

如果有任何问题，请查看 [故障排除文档](../references/troubleshooting)。
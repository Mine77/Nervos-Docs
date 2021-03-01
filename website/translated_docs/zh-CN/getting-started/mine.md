---
id: mine
title: 开始挖矿
---

现在你已经 [创建了一个钱包](wallet) 并且 [开始运行节点](run-node)，下一步是运行矿工程序来挖矿并获得一些CKB。

> 请注意，您应该等到 `ckb run` 进程同步到 [最新高度](https://explorer.nervos.org/)，再启动挖矿程序。

## 运行挖矿程序

CKB 的挖矿程序并未与 CKB 的主程序结合起来。 因此，要运行 CKB 挖矿程序，你需要打开另一个终端 shell，同时 **保持 `ckb run` 仍在运行**。

在节点配置文件夹 `ckb-testnet` 中打开另一个终端并运行：

```bash
ckb miner
```

现在，CKB 节点和挖矿程序应该都已经正常工作了。

等待片刻之后，当你看到这样的消息时，这意味着你已经开采出了一个新的块：

```bash
2019-05-02 12:19:23.463 +08:00 main INFO miner \
found seal: Seal { \
    nonce: 16607377657024071670, \
    proof: 0xa2020000681b00005d27000018340000973d000083430000fc600000376600008c660000cc6800007970000015760000 \
}
```

您可以在 [CKB Explorer](https://explorer.nervos.org/)上使用你的地址来查看您的CKB Token 余额。

如果有任何问题，请查看 [故障排除文档](../references/troubleshooting)。
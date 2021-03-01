---
id: introduction
title: 介绍
---

在本节中，您将学习如何在实践中使用 Nervos CKB。 这包括 [运行的CKB节点](run-node)， [与它交互](interact)，以及 [采矿](mine) 和 [发送交易](transfer) 。 <!-- Todo: change the version here -->

请注意，本文档与 `ckb 0.13.0（rylai-v2 v0.13.0 2019-06-01）`兼容。 关于CKB版本的更多信息可以参考 [GitHub 上 CKB 的 Repo](https://github.com/nervosnetwork/ckb)。

## 系统要求

任何现代计算机都应该能够运行CKB节点和挖矿程序。

推荐的操作系统：

* Ubuntu 18.04 LTS x86-64
* macOS

实验性支持的系统：

* Windows x86-64

理论上支持的系统：

* Ubuntu 16.04 LTS x86-64
* Arch Linux x86-64
* Centos 7 x86-64
* Debian x86-64, Stretch or later

如果你的操作系统还不被当前版本的 CKB 支持，您也可以 [使用 Docker](https://github.com/nervosnetwork/ckb/blob/develop/docs/run-ckb-with-docker.md) 来运行 CKB。

## 测试网

在开始使用测试网之前，您需要注意以下事项：

* CKB 测试网只用于开发和测试。
* 这个测试网上的 Token 几乎没有任何价值，所以请谨防诈骗。
* **测试网将每两周重置一次并进行更新**，因此测试网上的任何 Token 或状态都将在测试网重置时被清除。

## 预备知识

由于本文档中大部分的教程的都是基于命令行界面上的，你可能需要先了解 [如何在 您的计算机上使用命令行工具](https://www.google.com/search?q=learn+command+line)。
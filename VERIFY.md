# 校验下载文件

每个发行版都附带 `SHA256SUMS`。下载 DMG 后在终端运行：

```sh
shasum -a 256 ~/Downloads/Celia-0.0.6-arm64.dmg
```

输出的前一串字符应与 `SHA256SUMS` 中对应行完全一致，不一致请不要打开。

应用内更新使用单独的签名：发行版附带 `manifest.json` 与签名文件 `manifest.sig`，Celia 内置公钥，下载后先校验签名与哈希，通过才会更新。`release-public-key.pem` 是对应的公钥，可以与应用内置的公钥比对。

## 发行版里的其他文件
- `NOTICE.md`：第三方组件清单与许可证。
- `LGPL-REPLACEMENT.md` 与 `Celia-ThirdParty-Sources-*.tar.gz`：LGPL 组件的替换说明与对应源码。

## 较小的更新包

从 0.0.6 开始，Celia 也会核对 `delta-index.json` 和 `delta-index.sig`。它们由相同的发布密钥签名，列出适用旧版本、补丁大小与哈希，以及更新后每个文件清单的哈希。原来的 `manifest.json` 不变。

应用下载补丁后，在临时副本中核对所有文件、权限和链接，包含应用签名文件。核对失败就使用完整包；两条路径都须通过签名校验，并经过备份、启动检查和失败回退。首次提供此能力的 0.0.6 可以没有可用补丁，索引为空是正常的。

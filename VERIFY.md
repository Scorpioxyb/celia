# 校验下载文件

每个发行版都附带 `SHA256SUMS`。下载 DMG 后在终端运行：

```sh
shasum -a 256 ~/Downloads/Celia-1.0.0-arm64.dmg
```

输出的前一串字符应与 `SHA256SUMS` 中对应行完全一致，不一致请不要打开。

应用内更新使用单独的签名：发行版附带 `manifest.json` 与签名文件 `manifest.sig`，Celia 内置公钥，下载后先校验签名与哈希，通过才会更新。`release-public-key.pem` 是对应的公钥，可以与应用内置的公钥比对。

## 发行版里的其他文件
- `NOTICE.md`：第三方组件清单与许可证。
- `LGPL-REPLACEMENT.md` 与 `Celia-ThirdParty-Sources-*.tar.gz`：LGPL 组件的替换说明与对应源码。

# DualSubs YouTube Fixed / 修复版

> 中文：这是适用于 Surge 的 YouTube 双语字幕修复模块，重点处理 iOS YouTube App 中可能出现的“字幕加载失败”。
>
> English: A fixed Surge module for YouTube bilingual subtitles, focused on preventing subtitle-loading failures in the iOS YouTube app.

## 原作与署名 / Attribution

- 原项目 / Original projects: [DualSubs YouTube](https://github.com/DualSubs/YouTube) and [DualSubs Universal](https://github.com/DualSubs/Universal)
- 原作者 / Original author: [VirgilClyne](https://github.com/VirgilClyne) and DualSubs contributors
- 修复版维护 / Fixed release maintenance: Eugene-Prime
- 许可证 / License: 上游项目采用 Apache-2.0；本仓库保留上游署名并发布修改后的衍生产物。 / The upstream projects are Apache-2.0 licensed; this repository retains attribution and distributes modified derivative artifacts.

## 安装 / Install

1. 在 Surge 关闭所有其他 DualSubs YouTube 模块。/ Disable every other DualSubs YouTube module in Surge.
2. 添加模块：/ Add this module:

   `https://raw.githubusercontent.com/Eugene-Prime/YouTube-subtitle/main/release-surge/DualSubs.YouTube.Fixed.sgmodule?v=1.1.0-local`

3. 默认 `Type=Translate`，无需改动。/ Keep the default `Type=Translate`.
4. YouTube 内选择“字幕 → 自动翻译 → 中文（简体）”。/ In YouTube choose “Subtitles → Auto-translate → Chinese (Simplified)”.

完整的修复说明、限制和参数表见 [release-surge/README.md](release-surge/README.md)。 / See [release-surge/README.md](release-surge/README.md) for full repair notes, limitations, and parameter descriptions.

## 修复内容 / Fixes

- 阻止 Official 模式的内部字幕请求再次触发字幕处理链。/ Prevents Official-mode internal subtitle fetches from re-entering the subtitle pipeline.
- 翻译耗时过长时安全返回原字幕，避免 iOS YouTube 因超时显示“字幕加载失败”。/ Safely returns source captions when translation is slow, avoiding iOS YouTube's “subtitle loading failed” timeout.
- 支持 `youtubei-att.googleapis.com`，并注入中文（简体）自动翻译选项。/ Supports `youtubei-att.googleapis.com` and injects Chinese (Simplified) into Auto-translate.

## 文件 / Files

- [正式模块 / Production module](release-surge/DualSubs.YouTube.Fixed.sgmodule)
- [局域网测试模块 / LAN test module](release-surge/DualSubs.YouTube.Fixed.LAN.sgmodule)
- [校验和 / SHA-256 checksums](release-surge/SHA256SUMS.txt)


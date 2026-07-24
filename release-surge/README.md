# DualSubs YouTube Fixed / 修复版

> 中文：面向 Surge 的 YouTube 双语字幕修复模块，基于 DualSubs YouTube 与 DualSubs Universal 的公开代码和发布产物，重点修复 iOS YouTube App 的“字幕加载失败”。
>
> English: A fixed Surge module for YouTube bilingual subtitles, based on the public DualSubs YouTube and Universal projects. It targets the subtitle-loading failures seen in the iOS YouTube app.

## 原作与署名 / Attribution

- 原项目 / Original projects: [DualSubs YouTube](https://github.com/DualSubs/YouTube) and [DualSubs Universal](https://github.com/DualSubs/Universal)
- 原作者 / Original author: [VirgilClyne](https://github.com/VirgilClyne) and DualSubs contributors
- 修复版维护 / Fixed release maintenance: Eugene-Prime
- 许可证 / License: 上游项目采用 Apache-2.0；本仓库保留上游署名并发布修改后的衍生产物。 / The upstream projects are Apache-2.0 licensed; this repository retains attribution and distributes modified derivative artifacts.

## 修复内容 / What this fixes

- Official 模式的内部原字幕请求会清理 `tlang`、`subtype` 等标记，并以内部请求标记绕过再次改写，防止递归。/ Official-mode internal source-caption fetches clear DualSubs markers and bypass the subtitle pipeline to prevent recursion.
- Translate 模式设有六秒安全回退：翻译服务不能及时完成时，原字幕会直接返回，避免 iOS YouTube 在约八秒后取消 timedtext 请求并显示“字幕加载失败”。/ Translate mode has a six-second fail-open deadline: slow translation returns source captions before iOS YouTube cancels its timedtext request at roughly eight seconds.
- Player 和 GetWatch 规则覆盖 `youtubei-att.googleapis.com`。/ Player and GetWatch rules also cover `youtubei-att.googleapis.com`.
- 自动翻译菜单注入中文（简体）。/ Chinese (Simplified) is injected into Auto-translate.

## 安装 / Install

1. 关闭其他所有 DualSubs YouTube 模块。/ Disable all other DualSubs YouTube modules.
2. 在 Surge 添加：/ Add this URL in Surge:

   `https://raw.githubusercontent.com/Eugene-Prime/YouTube-subtitle/main/release-surge/DualSubs.YouTube.Fixed.sgmodule?v=1.1.0-local`

3. 保持默认 `Type=Translate`。/ Keep the default `Type=Translate`.
4. 在 YouTube 选择“字幕 → 自动翻译 → 中文（简体）”。/ In YouTube choose “Subtitles → Auto-translate → Chinese (Simplified)”.

## 平台状态 / Platform status

| 平台 / Platform | 文件 / Package | 状态 / Status |
| --- | --- | --- |
| Surge | `DualSubs.YouTube.Fixed.sgmodule` | **已在 iOS 实机测试 / Tested on iOS** |
| Loon | `DualSubs.YouTube.Fixed.Loon.plugin` | **未测试 / Untested** |
| Quantumult X | `DualSubs.YouTube.Fixed.QX.conf` | **未测试 / Untested** |
| Shadowrocket | `DualSubs.YouTube.Fixed.srmodule` | **未测试 / Untested** |
| Stash | `DualSubs.YouTube.Fixed.Stash.yaml` | **未测试 / Untested** |

除 Surge 外，其他文件根据上游模板适配并复用相同的修复 bundle，尚未经过实机验证。/ All non-Surge packages are adapted from upstream templates and reuse the same fixed bundles; they have not been device-tested.

Quantumult X 没有 Surge 的参数面板；使用 QX 版本前，请在 DualSubs/BoxJs 设置中确认 `Type=Translate`。/ Quantumult X has no Surge-style parameter panel; set `Type=Translate` in DualSubs/BoxJs before using the QX package.

## 参数说明 / Parameters

| 参数 / Parameter | 默认值 / Default | 说明 / Description |
| --- | --- | --- |
| `Type` | `Translate` | `Translate`（推荐）用翻译服务生成双语字幕。`Official` 合成 YouTube 官方译文与原文，可能受限流影响。`External` 用于外挂字幕。 / `Translate` (recommended) creates bilingual subtitles with a translation service. `Official` combines YouTube's translated and source captions and can be rate-limited. `External` is for external subtitle sources. |
| `AutoCC` | `true` | 自动为原字幕添加已选择的目标语言；首次请在播放器手动选择中文（简体）。 / Automatically requests the remembered target language; choose Chinese (Simplified) manually the first time. |
| `Position` | `Forward` | `Forward` 原文在上、译文在下；`Reverse` 相反。 / `Forward` places source above translation; `Reverse` does the opposite. |
| `Vendor` | `Google` | 翻译服务。Google 为默认；Microsoft、DeepL 等需要自行在 DualSubs/BoxJs 配置有效凭据。 / Translation provider. Google is the default; Microsoft, DeepL, and similar services require valid credentials in DualSubs/BoxJs. |
| `ShowOnly` | `false` | `true` 仅显示译文；`false` 显示双语。 / `true` shows translation only; `false` shows bilingual captions. |
| `Debug` | `false` | 输出 Surge 脚本诊断日志；排障结束请关闭。 / Enables Surge script diagnostics; turn it off after troubleshooting. |
| `LogLevel` | `WARN` | 日常建议 `WARN`；仅排障时使用 `DEBUG`。 / Use `WARN` normally and `DEBUG` only while diagnosing. |

## 限制 / Limits

长视频的在线翻译可能无法在 App 等待期限内完成；本修复版会回退原字幕而不是让字幕整体失败。/ Online translation for long videos may not complete before the app deadline; this release falls back to source captions instead of breaking subtitles altogether.

不要同时启用多个会改写 YouTube Player 或 TimedText 响应的模块。/ Do not enable multiple modules that modify YouTube Player or TimedText responses simultaneously.

## 局域网测试 / LAN test

1. 在本目录运行 `python3 -m http.server 8080 --directory .`。
2. 将 `DualSubs.YouTube.Fixed.LAN.sgmodule` 中的 `REPLACE_LAN_IP` 替换成 Mac 的局域网 IP。
3. 将该模块导入 Surge 测试。

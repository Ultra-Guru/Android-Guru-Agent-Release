<a id="readme-top"></a>
<div align="center">

# Android Guru Agent · Release

### 📦 发布仓库 —— 全部更新资产与客户端清单的唯一权威来源

[Android-Guru-Agent](https://github.com/Ultra-Guru/Android-Guru-Agent) 的产物通道：APK / vcdiff 增量补丁 / 热更包
与三份客户端清单（版本 / 补丁索引 / 更新日志）都在这里，**不含源码**。

**状态**

<a href="https://github.com/Ultra-Guru/Android-Guru-Agent-Release/releases/latest"><img src="https://img.shields.io/github/v/release/Ultra-Guru/Android-Guru-Agent-Release?style=flat-square&color=2ea44f&label=%E6%9C%80%E6%96%B0%E7%89%88%E6%9C%AC" alt="Latest Release"/></a>
<a href="https://github.com/Ultra-Guru/Android-Guru-Agent-Release/actions/workflows/validate-manifests.yml"><img src="https://github.com/Ultra-Guru/Android-Guru-Agent-Release/actions/workflows/validate-manifests.yml/badge.svg?branch=main" alt="Validate Manifests"/></a>
<img src="https://img.shields.io/github/downloads/Ultra-Guru/Android-Guru-Agent-Release/total?style=flat-square&color=blueviolet&label=%E4%B8%8B%E8%BD%BD%E9%87%8F" alt="Downloads"/>
<img src="https://img.shields.io/github/releases/Ultra-Guru/Android-Guru-Agent-Release?style=flat-square&color=orange&label=%E5%8F%91%E5%B8%83%E6%AC%A1%E6%95%B0" alt="Releases"/>
<img src="https://img.shields.io/badge/platform-Android_8.0%2B-3DDC84?logo=android&logoColor=white" alt="Platform"/>

**快速跳转**

<a href="#-下载-apk"><img src="https://img.shields.io/badge/⬇️_下载_APK-最新版-2ea44f" alt="Download"/></a>
<a href="#️-全自动发布流程"><img src="https://img.shields.io/badge/⚙️_发布流程-全自动-1F6FEB" alt="Pipeline"/></a>
<a href="#️-三通道更新优先级"><img src="https://img.shields.io/badge/🛰️_更新通道-热更·增量·全量-8A2BE2" alt="Channels"/></a>
<a href="#-客户端接入点"><img src="https://img.shields.io/badge/🔌_客户端接入-固定读取点-0077B5" alt="Client API"/></a>
<a href="./HOT_UPDATE.md"><img src="https://img.shields.io/badge/🔥_热更手册-HOT_UPDATE-E95420" alt="Hot Update"/></a>

</div>

---

## 📥 下载 APK

**→ 永远指向最新版：[Releases 最新发布页](https://github.com/Ultra-Guru/Android-Guru-Agent-Release/releases/latest)**

| 变体 | 适用设备 | 体积 | 直链规律 |
| --- | --- | --- | --- |
| `*-arm64-*.apk` | 现代手机（arm64-v8a）· **首选** | ~325 MB | `ApexAgent-v<版本>-release-arm64-<commit>.apk` |
| `*-universal-*.apk` | 旧设备 / 模拟器（全 ABI 兜底） | ~912 MB | `ApexAgent-v<版本>-release-universal-<commit>.apk` |

> - 文件名中的 `<commit>` 为构建该 APK 的开发仓库 commit 前 8 位，可与 `version.json` 的 `commitSha` 对照溯源；
> - 两个变体均内置 Ubuntu 24.04 完整 CLI 环境（gcc / python3 / git / vim 开箱即用），首次使用离线解包约 2~5 分钟，零网络依赖；
> - 全部资产带 SHA-256（见 `version.json`），下载后可自行校验。

<details>
<summary><b>已安装旧版？—— 三种升级方式（App 会自动选最优）</b></summary>

| 你的情况 | 推荐方式 |
| --- | --- |
| 装了任意旧版（官方渠道） | App「设置 → 关于 → 检查更新」→ 自动增量（~20 MB 级）或全量 |
| 数据层小版本（技能 / MCP 目录变更） | App 内直接弹「热更新 · 免安装」卡片，即时生效 |
| 本地自编译 / 分叉构建 | 下载全量包覆盖安装；签名不一致时安装器会提示（见 [HOT_UPDATE.md](./HOT_UPDATE.md) 的签名预检说明） |

</details>

---

## 🗂️ 这里有什么

| 内容 | 说明 |
| --- | --- |
| **[Releases](https://github.com/Ultra-Guru/Android-Guru-Agent-Release/releases)** | 每版 APK（arm64 / universal）、多基底增量补丁与热更包 |
| **[version.json](./version.json)** | 最新版本清单：版本号 / 下载地址 / SHA-256 / 热更档 / 签名证书指纹 —— App「检查更新」的固定读取点 |
| **[patches.json](./patches.json)** | 历史补丁全量索引（from→to 全链）—— App 跨版本链式增量的数据底座 |
| **[changelog.json](./changelog.json)** | 更新日志清单（一级手动日志 + 二级 PR 分组 + 配图）—— App 升级后首启弹窗与「关于 → 更新日志」的数据源 |
| **[HOT_UPDATE.md](./HOT_UPDATE.md)** | 热更新通道规范与发布手册（hot 包格式 / version.json 新字段 / **应急热修操作手册** / FAQ） |
| **清单校验门禁** | `.github/workflows/validate-manifests.yml` —— 清单结构 / 自洽 / 单调性守门，任何写入（CI 自动提交 / hotfix 重发 / 人工修正）都强制复核 |
| **应急热修工作流** | `.github/workflows/hotfix.yml` —— 数据层坏内容紧急重发（零 APK 发版，约 2 分钟送达全部客户端） |

> 源代码、Issue、PR 请移步开发仓库：**https://github.com/Ultra-Guru/Android-Guru-Agent**

---

## ⚙️ 全自动发布流程

```
开发仓库 PR 合并进 main（或 push tag v*.*.*）
        │
        ▼
开发仓库 release.yml 构建 APK（universal + arm64，串行队列防并发）
        │
        ├─ 生成 version.json（SHA-256 / 签名证书指纹 / commit 溯源）
        ├─ 与最近 10 个版本各生成 xdelta3 增量补丁（LZMA 二级压缩，
        │   窗口内任意版本一步直达本版）
        ├─ 累积维护 patches.json（历史补丁全量索引）
        ├─ 聚合 .changelog/unreleased 片段 → changelog.json
        │   （发布器 App 手写日志 + PR 合并内容 + 配图，三落点发布）
        ├─ data-only 判定：本版变更全在热载路径（assets/skills、
        │   assets/mcp_catalog）→ 额外产出热更包 hot_v*.zip（免安装通道）
        ▼
通过跨仓库 PAT 发布到本仓库
        │
        ├─ 创建 Release + 上传 APK / 补丁 / 热更包 / 清单
        └─ 提交 version.json + patches.json + changelog.json 到 main
        │
        ▼
本仓库 validate-manifests 门禁自动复核（结构 / 自洽 / 单调性）
```

### 更新日志从哪来？

[apex-Administrator](https://github.com/Ultra-Guru/apex-Administrator)（更新日志发布器）是手机端管理工具：
随时随地写日志、**附配图截图**，一键提交到开发仓库 `.changelog/unreleased/` —— 提交即触发上面的发版流水线，
新版 App 升级后首启弹窗即展示该日志（v1.4.7+ 支持配图展示）。

### 应急热修（本仓库独立执行，不走开发仓库发版）

已发布版本的数据层（技能 / 目录）出了坏内容时：开发仓库合入仅触碰 assets 数据的修复 →
本仓库 Actions → **Emergency hot update** → 工作流打包快照、挂到当前版本 Release、重写 hot 档
（target 不变 + 新指纹）→ 客户端凭包指纹自动重新应用（零安装）。白名单守卫与开发仓库 CI 同尺：
含代码变更的修复拒绝走此通道。操作手册见 **[HOT_UPDATE.md](./HOT_UPDATE.md)**「应急热修」一节。

---

## 🛰️ 三通道更新优先级

App（v1.4.7+）检查更新后按以下优先级自动选择通道：

| 优先级 | 通道 | 适用 | 是否安装 |
| --- | --- | --- | --- |
| 1 | **热更新**（`version.json` 的 `hot` 档） | data-only 版本（只改技能 / MCP 目录）与应急修订 | **零安装，下载后即时生效** |
| 2 | **增量补丁**（vcdiff） | 官方渠道安装且签名一致 | 合成新 APK 后系统安装器确认 |
| 3 | **全量包** | 兜底 | 系统安装器确认 |

> **增量更新（v1.4.5+）**：App 下载补丁后在应用内**自动合成新 APK 并拉起安装**（内置纯 Kotlin VCDIFF 解码器，
> 无需命令行、无需 xdelta3）；跨任意多个小版本时自动按 `patches.json` 解析补丁链逐段应用，
> 链体积超过全量包 60% 时才回退全量。
>
> **热更新（v1.4.7+）**：本版只改了数据层（技能 / MCP 目录）时，App 直接出现「热更新 · 免安装」卡片 ——
> 下载几 MB 的 `hot_v*.zip`，校验落位后技能与目录**即时生效**。全程不碰 APK、不做签名校验 ——
> **本地构建 / 分叉构建用户从此不再撞签名冲突**。数据层发布后发现问题可**同版本应急重发**
> （本仓库 hotfix 工作流，客户端凭包指纹自动重新应用）。含代码变更的版本仍走增量 / 全量，
> 且 App 会比对 `version.json` 的 `signingCertSha256` 与本地签名指纹，不一致时**提前警告**
> （不再下载几百 MB 后才在安装器里报错）。详见 **[HOT_UPDATE.md](./HOT_UPDATE.md)**。

---

## 🔌 客户端接入点

三份清单固定从本仓库 main 分支读取（raw CDN 零鉴权，公开仓库无需 Token）：

```
https://raw.githubusercontent.com/Ultra-Guru/Android-Guru-Agent-Release/main/version.json
https://raw.githubusercontent.com/Ultra-Guru/Android-Guru-Agent-Release/main/patches.json
https://raw.githubusercontent.com/Ultra-Guru/Android-Guru-Agent-Release/main/changelog.json
```

<details>
<summary><b>changelog.json 结构速览（apex-changelog-v3）</b></summary>

```jsonc
{
  "schema": "apex-changelog-v3",
  "latest": {                          // 当前最新版（弹窗首选内容源）
    "versionName": "1.4.9.57",
    "versionCode": 133,
    "date": "2026-10-24",
    "title": "v1.4.9.57 更新内容",
    "notes": ["……"],                  // 一级日志（发布器手写要点）→ 弹窗置顶
    "images": ["https://…/1.jpg"],     // 配图（发布器附图）→ 弹窗要点下方图廊
    "pr": [{ "title": "…", "notes": ["…"] }],   // 二级日志（PR 合并内容分组）
    "markdown": "…",                   // 全量底稿（两级均空时的纯文本降级）
    "releaseUrl": "https://…/tag/v1.4.9.57"
  },
  "history": [ /* 历史条目，最新在前，封顶 50 条 */ ]
}
```

- 全字段可缺省 + 客户端忽略未知字段 —— schema 演进不崩老客户端，老清单不崩新客户端；
- `images`（v3 新增）：发布器发送片段时附带的配图 URL 列表，App 弹窗内图廊展示、点开放大。

</details>

<details>
<summary><b>version.json 结构速览</b></summary>

```jsonc
{
  "versionName": "1.4.9.57",
  "versionCode": 133,                  // 只增不减（门禁强制单调）
  "tag": "v1.4.9.57",
  "publishedAt": "2026-10-24T12:58:49Z",
  "releasePage": "https://…/tag/v1.4.9.57",
  "download": {
    "arm64":     { "url": "…", "sizeBytes": 341151334, "sha256": "…" },
    "universal": { "url": "…", "sizeBytes": 956075252, "sha256": "…" }
  },
  "patch": {                            // 单补丁档只收 primary（上一版 → 本版）
    "arm64":     { "fromTag": "v1.4.9.56", "url": "…", "sizeBytes": 11125198, "sha256": "…" },
    "universal": { "fromTag": "v1.4.9.56", "url": "…", "sizeBytes": 11117347, "sha256": "…" }
  },
  "hot": {                              // 热更档（data-only 版本出现，见 HOT_UPDATE.md）
    "url": "…", "baseVersionCode": 132, "targetVersionCode": 133, "targetVersionName": "…"
  },
  "commitSha": "…",                     // 构建该 APK 的开发仓库完整 SHA
  "signingCertSha256": "…"              // 签名预检指纹（提前警告签名不一致）
}
```

</details>

---

## 🤝 相关仓库

| 仓库 | 角色 |
| --- | --- |
| [Android-Guru-Agent](https://github.com/Ultra-Guru/Android-Guru-Agent) | 开发仓库 —— 源代码 / Issue / PR |
| **本仓库** | 发布仓库 —— 产物与客户端清单（你在这里） |
| [apex-Administrator](https://github.com/Ultra-Guru/apex-Administrator) | 更新日志发布器 —— 手机端写日志 / 附配图，一键触发发版 |

---

*本仓库由 [release.yml](https://github.com/Ultra-Guru/Android-Guru-Agent/blob/main/.github/workflows/release.yml) 全自动维护 —— 人工提交请走 PR（validate-manifests 门禁强制校验后合并）。*

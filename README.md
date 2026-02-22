# Doubao TTS — Raycast Extension

<p align="center">
  <img src="assets/icon.png" width="128" height="128" alt="Doubao TTS Icon" />
</p>

<p align="center">
  在 macOS 上选中任意文字，通过 <a href="https://www.raycast.com/">Raycast</a> 一键朗读。<br/>
  基于<a href="https://www.volcengine.com/docs/6561/1598757">火山引擎豆包语音合成大模型 V3</a>，无需安装豆包 App。
</p>

---

## 为什么需要这个扩展？

火山引擎的豆包 TTS 提供了高质量的中文语音合成能力，但官方只提供了豆包 App 或复杂的 SDK 集成方式。本扩展通过直接调用 V3 HTTP API，让你在 Raycast 中即可使用：

- **科研工作者**：朗读论文、文档，解放双眼
- **语言学习者**：听取标准中文发音
- **内容创作者**：快速预览文本的语音效果
- **任何需要 TTS 的人**：无需安装额外 App，选中文字即可朗读

## 功能特性

- 🎙️ **Quick Read** — 选中文字，一键朗读（无界面，即时播放）
- 🎛️ **Voice Selection** — 从 90+ 音色中选择（按分类浏览）
- ⏹️ **Stop Reading** — 随时停止播放
- 🔄 **Toggle 模式** — 再次触发 Quick Read 即可停止当前播放
- 📊 **智能分片** — 自动将长文本按句子拆分，逐片合成播放
- ⚡ **模型版本切换** — 支持 TTS 2.0（推荐）和 TTS 1.0
- 🌐 **中英文支持** — 内置中文和英文音色

## 安装

### 前置要求

- [Raycast](https://www.raycast.com/) 已安装
- 火山引擎账号，已开通**豆包语音合成**服务（[开通指南](#获取-app-id-和-access-key)）

### 安装步骤

```bash
# 1. 克隆仓库
git clone https://github.com/xwzhangSZU/raycast-doubao-tts.git
cd raycast-doubao-tts

# 2. 安装依赖
npm install

# 3. 启动开发模式（自动加载到 Raycast）
npm run dev
```

启动后，在 Raycast 中搜索 "Doubao" 即可看到命令。

## 配置

首次使用时，Raycast 会自动弹出偏好设置页面。你需要配置以下信息：

| 配置项 | 说明 | 必填 |
|--------|------|:----:|
| **App ID** | 火山引擎应用标识 | ✅ |
| **Access Key** | 火山引擎访问密钥 | ✅ |
| 模型版本 | 语音合成模型（默认 2.0 推荐） | |
| Default Voice | Quick Read 使用的默认音色 | |
| Speech Rate | 语速（0.5x ~ 2.0x） | |

### 获取 App ID 和 Access Key

1. 注册并登录 [火山引擎控制台](https://console.volcengine.com/)
2. 进入 [语音技术 → 豆包语音合成](https://console.volcengine.com/speech/service/10007)
3. 如尚未开通，点击「开通服务」
4. 在控制台页面获取：
   - **App ID**：即 `X-Api-App-Id`
   - **Access Key**（Access Token）：即 `X-Api-Access-Key`
5. 详细步骤参考：[控制台使用 FAQ](https://www.volcengine.com/docs/6561/196768)

> **提示**：火山引擎新用户有免费额度，具体以控制台显示为准。

### 模型版本

| 模型版本 | Resource ID | 说明 |
|----------|-------------|------|
| 豆包语音合成 2.0（推荐） | `seed-tts-2.0` | 最新模型，音质更好 |
| 豆包语音合成 1.0 | `seed-tts-1.0` | 经典模型，音色更多 |
| 豆包语音合成 1.0（并发版） | `seed-tts-1.0-concurr` | 支持更高并发 |
| 声音复刻 2.0 | `seed-icl-2.0` | 声音克隆 |
| 声音复刻 1.0 | `seed-icl-1.0` | 声音克隆 |

> **注意**：不同模型版本支持不同音色。选择 2.0 模型时只显示 2.0 音色，选择 1.0 模型时只显示 1.0 音色。

### 音色列表

扩展内置了 90+ 音色，按以下分类组织：

| 分类 | 示例音色 | 模型版本 |
|------|----------|----------|
| 通用女声 | Vivi、小何、灿灿、亲切女声 | 1.0 / 2.0 |
| 通用男声 | 云舟、小天、擎苍、阳光青年 | 1.0 / 2.0 |
| 多情感女声 | 多情感灿灿、甜美女声 | 1.0 |
| 多情感男声 | 多情感男声 | 1.0 |
| 英文音色 | Tim、Adam、Amanda | 1.0 / 2.0 |
| 日语 / 韩语 / 多语种 | 日语女声、韩语女声 | 1.0 / 2.0 |
| 趣味口音 / 角色扮演 | 东北老铁、京腔侃爷、奶气萌娃 | 1.0 |

完整音色列表：[豆包大模型音色列表](https://www.volcengine.com/docs/6561/1257544)

## 使用方法

### Quick Read（推荐）

1. 在任意应用中选中文字
2. 打开 Raycast（默认 `⌥ Space`）
3. 输入 `Quick Read` 并回车
4. 开始朗读！再次触发同一命令即可停止

### Read with Voice Selection

1. 选中文字
2. 在 Raycast 中打开 `Read with Voice Selection`
3. 浏览音色列表，选择喜欢的音色
4. 按回车开始朗读

### Stop Reading

- 在 Raycast 中执行 `Stop Reading` 命令
- 或在 Quick Read 播放时再次触发 Quick Read

## 开发

### 项目结构

```
raycast-doubao-tts/
├── src/
│   ├── api/
│   │   ├── volcengine-tts.ts   # V3 API 客户端
│   │   └── types.ts            # TypeScript 类型定义
│   ├── constants/
│   │   └── voices.ts           # 90+ 音色配置
│   ├── utils/
│   │   ├── audio-player.ts     # 音频播放器（afplay）
│   │   └── text-chunker.ts     # 文本智能分片
│   ├── quick-read.tsx          # Quick Read 命令
│   ├── read-with-voice.tsx     # 音色选择命令
│   └── stop-reading.tsx        # 停止播放命令
├── assets/
│   └── icon.png                # 扩展图标
├── package.json                # 扩展配置 & 偏好设置
└── tsconfig.json
```

### 本地开发

```bash
npm install    # 安装依赖
npm run dev    # 开发模式（热重载）
npm run build  # 构建
npm run lint   # 代码检查
```

### 技术细节

- **API**：调用火山引擎豆包 TTS V3 HTTP 单向流式接口
- **认证**：通过 HTTP Headers（`X-Api-App-Id`、`X-Api-Access-Key`、`X-Api-Resource-Id`）
- **响应格式**：JSON Lines（NDJSON），每行一个 JSON 对象
- **音频格式**：MP3, 24000 Hz
- **文本分片**：按句号/逗号等标点智能拆分，每片 ≤ 1024 UTF-8 字节
- **播放**：使用 macOS 内置 `afplay` 命令
- **跨命令停止**：通过 PID 文件（`$TMPDIR/doubao-tts.pid`）实现

## 相关文档

- [Raycast 扩展开发文档](https://developers.raycast.com/)
- [豆包语音合成大模型 V3 HTTP 接口](https://www.volcengine.com/docs/6561/1598757)
- [豆包大模型音色列表](https://www.volcengine.com/docs/6561/1257544)
- [火山引擎控制台 FAQ](https://www.volcengine.com/docs/6561/196768)

## 致谢

- [Bob Plugin - 豆包 TTS](https://github.com/Littlecowherd/bob-plugin-doubao-tts) — 本项目参考了其配置方案
- [火山引擎](https://www.volcengine.com/) — 提供豆包语音合成 API

## 许可证

[MIT](LICENSE)

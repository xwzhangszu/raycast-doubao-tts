# Doubao TTS — Raycast 扩展

<p align="center">
  <img src="assets/command-icon.png" width="128" height="128" alt="Doubao TTS 图标" />
</p>

<p align="center">
  在 macOS 上选中任意文字，通过 <a href="https://www.raycast.com/">Raycast</a> 一键朗读，基于<a href="https://www.volcengine.com/docs/6561/1329505">火山引擎豆包语音合成大模型 V3 WebSocket 双向流式接口</a>。
</p>

---

## 为什么选择 Doubao TTS？

Doubao TTS 是火山引擎提供的 AI 语音合成服务，适合中文、英文和多语种文本朗读。本扩展把豆包语音接入 Raycast，让你可以直接朗读论文、网页文章、笔记、技术文档和日常选中文字，不需要离开当前 macOS 工作流。扩展调用的是火山引擎 OpenSpeech 接口，并使用 `seed-tts-2.0`、`seed-tts-1.0`、`seed-icl-2.0` 等豆包 TTS 模型/资源 ID。

## 本次更新

- **接入新版 V3 传输接口**：语音合成改为火山引擎豆包 TTS V3 WebSocket 双向流式接口，地址为 `wss://openspeech.bytedance.com/api/v3/tts/bidirection`。
- **支持新版控制台鉴权**：新用户可以直接填写火山引擎 `X-Api-Key`。
- **保留旧凭证兼容**：如果 API Key 为空，已有用户仍可继续使用 App ID + Access Key。
- **优化性能**：文本分片上限提升到 4096 UTF-8 字节，中等长度文章会减少不必要的 WebSocket 会话；播放当前分片时会预合成下一分片。
- **停止更干净**：停止播放时会同步取消后台预合成任务。
- **扩展音色覆盖**：音色选择器对齐官方豆包 TTS 2.0 音色目录，内置 160+ 个中英文音色。
- **更新图标**：替换了扩展图标，并提供浅色/深色主题图标资源。

## 适用人群

- **研究者**：朗读论文、摘录和笔记，减轻长时间阅读负担。
- **开发者**：听取 README、文档和长注释，换一种方式审阅文本。
- **语言学习者**：听取中文、英文发音示例。
- **内容创作者**：快速试听不同音色下的文本效果。
- **日常用户**：选中文字，触发 Raycast，即可朗读。

## 功能特性

- **一键朗读**：选中文字后快速朗读，无需打开视图。
- **音色选择**：按分类浏览 160+ 个音色，包含官方豆包语音合成模型 2.0 音色列表。
- **Quick Read 音色选择**：选择、试听并重置 Quick Read 默认音色。
- **停止播放**：随时停止播放，也可以再次触发 Quick Read 来停止。
- **智能分片**：按句子和标点拆分长文本。
- **流水线播放**：当前分片播放时，后台预合成下一分片。
- **模型切换**：支持豆包 TTS 2.0、TTS 1.0、TTS 1.0 高并发和声音复刻资源 ID。
- **灵活鉴权**：优先使用当前火山引擎 `X-Api-Key` 鉴权方式，并保留旧版 App ID / Access Key 兼容。
- **音色/模型兼容过滤**：根据所选模型/资源 ID 展示兼容音色。

## 截图

![Doubao TTS 截图](metadata/doubao-tts-1.png)

## 安装

### 前置要求

- 已安装 [Raycast](https://www.raycast.com/)
- 已开通火山引擎豆包语音合成服务

### 安装步骤

1. 从 Raycast Store 安装 **Doubao TTS**。
2. 打开扩展偏好设置。
3. 填写新版火山引擎控制台中的 **API Key**；已有用户也可以继续使用 App ID 和 Access Key。
4. 选择要使用的模型/资源 ID。默认是 `seed-tts-2.0`。
5. 为 **Quick Read Selected Text** 绑定快捷键，获得最快的朗读流程。

## 配置

首次使用前，请打开扩展偏好设置，并配置一种鉴权方式。

| 配置项 | 说明 | 必填 |
| --- | --- | :---: |
| API Key | 豆包语音 API Key，新版控制台推荐使用，会作为 `X-Api-Key` 发送。 | 推荐 |
| App ID | 旧版豆包 TTS App ID，仅在 API Key 为空时使用。 | 可选 |
| Access Key | 旧版豆包 TTS Access Key，仅在 API Key 为空时使用。 | 可选 |
| Model Version | 语音合成模型/资源 ID，默认 TTS 2.0。 | 可选 |
| Default Voice | Quick Read 默认音色。 | 可选 |
| Speech Rate | 语速，0.5x 到 2.0x。 | 可选 |

如果使用新版火山引擎控制台，只需要填写 **API Key**。如果 API Key 为空，扩展会自动回退到旧版 **App ID** + **Access Key** 请求头，方便已有用户平滑升级。

### 模型版本

| 模型 | Resource ID | 说明 |
| --- | --- | --- |
| Doubao TTS 2.0 | `seed-tts-2.0` | 默认推荐，仅显示兼容的 2.0 音色。 |
| Doubao TTS 1.0 | `seed-tts-1.0` | 经典 TTS 1.0 音色。 |
| Doubao TTS 1.0 高并发 | `seed-tts-1.0-concurr` | TTS 1.0 高并发资源。 |
| Voice Clone 2.0 | `seed-icl-2.0` | 声音复刻 2.0 资源。 |
| Voice Clone 1.0 | `seed-icl-1.0` | 声音复刻 1.0 资源。 |

不同资源 ID 支持的音色不同。扩展会根据当前选择的模型族过滤音色列表。

## 使用方法

### Quick Read

1. 在任意 macOS 应用中选中文字。
2. 打开 Raycast，运行 **Quick Read Selected Text**。
3. 再次触发该命令即可停止播放。

### 绑定快捷键

1. 打开 Raycast，搜索 **Extensions**。
2. 找到 **Doubao TTS**。
3. 为 **Quick Read Selected Text** 录制快捷键。
4. 之后在任意应用中选中文字并按下快捷键即可朗读。

也可以为 **Stop Reading** 绑定快捷键，方便快速停止。

### 选择 Quick Read 默认音色

1. 运行 **Select Quick Read Voice**。
2. 搜索或浏览当前模型支持的音色。
3. 按回车或使用 **Set as Quick Read Voice** 设置为默认朗读音色。
4. 使用 **Preview Voice** 可以用当前选区或剪贴板文本试听。
5. 使用 **Reset to Preference Default** 可恢复扩展偏好设置中的默认音色。

### 指定音色朗读

1. 选中文字。
2. 运行 **Read with Voice Selection**。
3. 选择音色并按回车朗读。

### 停止播放

- 在 Raycast 中运行 **Stop Reading**。
- 或在播放时再次触发 **Quick Read Selected Text**。

## 开发

### 项目结构

```text
raycast-doubao-tts/
├── src/
│   ├── api/
│   │   ├── volcengine-tts.ts   # 火山引擎豆包 TTS V3 WebSocket 客户端
│   │   └── types.ts            # TypeScript 类型
│   ├── constants/
│   │   └── voices.ts           # 豆包音色目录
│   ├── utils/
│   │   ├── audio-player.ts     # 基于 afplay 的播放与停止控制
│   │   ├── pipelined-reading.ts # 预合成流水线
│   │   ├── text-chunker.ts     # 智能文本分片
│   │   └── voice-preferences.ts # Quick Read 音色覆盖配置
│   ├── quick-read.tsx
│   ├── read-with-voice.tsx
│   ├── select-voice.tsx
│   └── stop-reading.tsx
├── assets/
│   ├── command-icon.png
│   └── command-icon@dark.png
├── metadata/
├── package.json
└── tsconfig.json
```

### 本地开发

```bash
npm install
npm run dev
npm run build
npm run lint
```

## 技术细节

- **API**：火山引擎豆包 TTS V3 WebSocket 双向流式接口
- **接口地址**：`wss://openspeech.bytedance.com/api/v3/tts/bidirection`
- **鉴权**：`X-Api-Key` 或旧版 `X-Api-App-Id` + `X-Api-Access-Key`，并附带 `X-Api-Resource-Id` 和每次连接唯一的 `X-Api-Connect-Id`
- **响应**：V3 WebSocket 二进制帧，音频 payload 为流式 MP3 数据
- **音频**：MP3，24000 Hz，128 kbps
- **分片**：按标点智能拆分，每片不超过 4096 UTF-8 字节
- **播放流水线**：播放当前分片时后台合成下一分片
- **播放**：macOS 内置 `afplay`
- **停止控制**：共享 PID 文件 `$TMPDIR/doubao-tts.pid`

## 相关文档

- [Raycast 扩展文档](https://developers.raycast.com/)
- [豆包语音合成大模型 V3 WebSocket 双向流式](https://www.volcengine.com/docs/6561/1329505)
- [豆包大模型音色列表](https://www.volcengine.com/docs/6561/1257544)
- [ListSpeakers - 大模型音色列表（新接口）](https://www.volcengine.com/docs/6561/2160690)
- [火山引擎控制台 FAQ](https://www.volcengine.com/docs/6561/196768)

## 致谢

- [Bob Plugin - Doubao TTS](https://github.com/Littlecowherd/bob-plugin-doubao-tts) 启发了本扩展的配置思路。
- [Volcengine](https://www.volcengine.com/) 提供豆包语音合成 API。

## 许可证

[MIT](LICENSE)

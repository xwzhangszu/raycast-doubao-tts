# Doubao TTS — Raycast Extension

<p align="center">
  <img src="assets/command-icon.png" width="128" height="128" alt="Doubao TTS Icon" />
</p>

<p align="center">
  Select any text on macOS and read it aloud with <a href="https://www.raycast.com/">Raycast</a>, powered by <a href="https://www.volcengine.com/docs/6561/1329505">Volcengine Doubao TTS V3 WebSocket bidirectional streaming</a>.
</p>

---

## Why Doubao TTS?

Doubao TTS is Volcengine's AI speech synthesis service for natural, expressive Chinese and multilingual speech. This extension brings it into Raycast so you can listen to papers, articles, notes, documentation, and everyday selected text without leaving your current macOS workflow. The extension talks to Volcengine's OpenSpeech endpoint and uses Doubao TTS model/resource IDs such as `seed-tts-2.0`, `seed-tts-1.0`, and `seed-icl-2.0`.

## What's New

- **New Volcengine V3 transport**: synthesis now uses the Doubao TTS V3 bidirectional WebSocket API at `wss://openspeech.bytedance.com/api/v3/tts/bidirection`.
- **New console authentication**: new users can configure the Volcengine `X-Api-Key` flow directly.
- **Compatibility fallback**: existing App ID + Access Key setups continue to work when API Key is empty.
- **Better performance**: longer 4096-byte chunks reduce unnecessary WebSocket sessions for medium-length text, and lookahead synthesis prepares the next chunk while the current chunk is playing.
- **Cleaner stop behavior**: stopping playback also cancels in-flight lookahead synthesis.
- **Expanded voice coverage**: the selector is aligned with the official Doubao TTS 2.0 catalog and includes 160+ Chinese and English voices.
- **Refreshed icon**: the extension icon has been updated with light and dark variants for Raycast.

## Who Is This For?

- **Researchers**: listen to papers, excerpts, and notes while reviewing or editing.
- **Developers**: review documentation, READMEs, and long comments by ear.
- **Language learners**: hear standard Chinese and English voice output.
- **Content creators**: quickly preview how text sounds in different voices.
- **Everyday users**: select text, trigger Raycast, and listen.

## Features

- **Quick Read**: select text and read it aloud instantly without opening a view.
- **Voice Selection**: browse 160+ voices organized by category, including the official Doubao TTS 2.0 voice catalog.
- **Select Quick Read Voice**: choose, preview, and reset the voice used by Quick Read.
- **Stop Reading**: stop playback anytime, or trigger Quick Read again to toggle playback off.
- **Smart Chunking**: split long text by sentence and punctuation.
- **Pipelined Playback**: synthesize the next text chunk while the current chunk is playing.
- **Model Switching**: supports Doubao TTS 2.0, TTS 1.0, high-concurrency 1.0, and voice clone resource IDs.
- **Flexible Auth**: uses the current Volcengine `X-Api-Key` flow, with legacy App ID and Access Key fallback.
- **Voice-Model Compatibility**: filters voices by the selected model/resource ID.

## Screenshots

![Doubao TTS Screenshot](metadata/doubao-tts-1.png)

## Installation

### Prerequisites

- [Raycast](https://www.raycast.com/) installed
- A Volcengine account with Doubao TTS enabled

### Setup

1. Install **Doubao TTS** from the Raycast Store.
2. Open the extension preferences.
3. Fill **API Key** from the current Volcengine Doubao Speech console, or keep using your existing App ID and Access Key.
4. Choose the model/resource ID you want to use. `seed-tts-2.0` is the default.
5. Bind a hotkey to **Quick Read Selected Text** for the fastest workflow.

## Configuration

Open the extension preferences before first use and configure one authentication method.

| Setting | Description | Required |
| --- | --- | :---: |
| API Key | Volcengine Doubao Speech API Key. Preferred for new users and sent as `X-Api-Key`. | Recommended |
| App ID | Legacy Volcengine TTS App ID, used only when API Key is empty. | Optional |
| Access Key | Legacy Volcengine TTS Access Key, used only when API Key is empty. | Optional |
| Model Version | TTS model/resource ID. Defaults to Doubao TTS 2.0. | Optional |
| Default Voice | Voice used by Quick Read when no override is selected. | Optional |
| Speech Rate | Playback speed from 0.5x to 2.0x. | Optional |

If you use the new Volcengine console, fill **API Key**. If API Key is empty, the extension falls back to legacy **App ID** + **Access Key** headers for existing users.

### Model Versions

| Model | Resource ID | Notes |
| --- | --- | --- |
| Doubao TTS 2.0 | `seed-tts-2.0` | Recommended default; only shows compatible 2.0 voices. |
| Doubao TTS 1.0 | `seed-tts-1.0` | Classic TTS 1.0 voices. |
| Doubao TTS 1.0 High Concurrency | `seed-tts-1.0-concurr` | TTS 1.0 high-concurrency resource. |
| Voice Clone 2.0 | `seed-icl-2.0` | Voice clone 2.0 resource ID. |
| Voice Clone 1.0 | `seed-icl-1.0` | Voice clone 1.0 resource ID. |

Different resource IDs support different voices. The extension filters the voice list to match the selected model family.

## Usage

### Quick Read

1. Select text in any macOS app.
2. Open Raycast and run **Quick Read Selected Text**.
3. Trigger the command again to stop playback.

### Bind a Hotkey

1. Open Raycast and search **Extensions**.
2. Find **Doubao TTS**.
3. Record a hotkey for **Quick Read Selected Text**.
4. Select text anywhere and press the hotkey to read it aloud.

You can also bind a hotkey to **Stop Reading**.

### Select the Quick Read Voice

1. Run **Select Quick Read Voice**.
2. Search or browse voices compatible with the selected model.
3. Press Enter or use **Set as Quick Read Voice** to set the selected voice.
4. Use **Preview Voice** to audition a voice with selected or clipboard text.
5. Use **Reset to Preference Default** to return to the default voice from extension preferences.

### Read with a Specific Voice

1. Select text.
2. Run **Read with Voice Selection**.
3. Pick a voice and press Enter to read.

### Stop Reading

- Run **Stop Reading** in Raycast.
- Or trigger **Quick Read Selected Text** again while playback is active.

## Development

### Project Structure

```text
raycast-doubao-tts/
├── src/
│   ├── api/
│   │   ├── volcengine-tts.ts   # Volcengine Doubao TTS V3 WebSocket client
│   │   └── types.ts            # TypeScript types
│   ├── constants/
│   │   └── voices.ts           # Doubao voice catalog
│   ├── utils/
│   │   ├── audio-player.ts     # afplay-based audio player and stop control
│   │   ├── pipelined-reading.ts # lookahead synthesis pipeline
│   │   ├── text-chunker.ts     # smart text chunking
│   │   └── voice-preferences.ts # Quick Read voice override
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

### Local Development

```bash
npm install
npm run dev
npm run build
npm run lint
```

## Technical Details

- **API**: Volcengine Doubao TTS V3 WebSocket bidirectional streaming
- **Endpoint**: `wss://openspeech.bytedance.com/api/v3/tts/bidirection`
- **Auth**: `X-Api-Key` or legacy `X-Api-App-Id` + `X-Api-Access-Key`, plus `X-Api-Resource-Id` and per-connection `X-Api-Connect-Id`
- **Response**: binary V3 WebSocket frames with streamed MP3 audio payloads
- **Audio**: MP3, 24000 Hz, 128 kbps
- **Chunking**: smart split by punctuation, up to 4096 UTF-8 bytes per chunk
- **Playback Pipeline**: one chunk plays while the next chunk is synthesized in the background
- **Playback**: macOS built-in `afplay`
- **Stop Control**: shared PID file at `$TMPDIR/doubao-tts.pid`

## References

- [Raycast Extension Docs](https://developers.raycast.com/)
- [Doubao TTS V3 WebSocket Bidirectional API](https://www.volcengine.com/docs/6561/1329505)
- [Doubao Voice Catalog](https://www.volcengine.com/docs/6561/1257544)
- [ListSpeakers - New Voice Catalog API](https://www.volcengine.com/docs/6561/2160690)
- [Volcengine Console FAQ](https://www.volcengine.com/docs/6561/196768)

## Acknowledgements

- [Bob Plugin - Doubao TTS](https://github.com/Littlecowherd/bob-plugin-doubao-tts) inspired the configuration approach.
- [Volcengine](https://www.volcengine.com/) provides the Doubao TTS API.

## License

[MIT](LICENSE)

---

**中文文档**: [README.zh.md](README.zh.md)

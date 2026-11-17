# Bilingual Board · 双语聊天板

A chat board for two people sharing one computer: a Chinese speaker who is learning English and an English speaker (who may be learning Chinese).
Each message is translated, and English mistakes are marked with a red pen, with the reasons explained in Chinese.
Works on **Windows** and **macOS**. No accounts and no cloud needed. Chats stay on your computer.

两个人用同一台电脑聊天：一位中文母语者（在学英语），一位英语母语者。消息自动翻译，英文错误用红笔改，并有中文解释。支持 Windows 和 macOS，聊天记录只存在你自己的电脑上。

![cats](img/fawn-step.png)

**Try it online · 在线试用:** https://skot-chen.github.io/bilingual-board/
**English only · 纯英文界面:** https://skot-chen.github.io/bilingual-board/?lang=en (or click **EN only** at the top right; click **中/EN** to switch back)

**Each person on their own device · 各用各的设备:** the first time the web page opens, it asks who is using the device. After that, every message is sent as that person and shown on the right, and the speaker never switches. Ready-made links:
- Chinese speaker 中文母语者: https://skot-chen.github.io/bilingual-board/?me=zh
- English speaker: https://skot-chen.github.io/bilingual-board/?me=en&lang=en

To change it, tap the 🔒 name button above the message box (it asks before switching), or use ⚙️ Settings → *Who uses this device*. On one shared computer, choose *Shared* to switch speakers as before.
Each message shows the device it came from (📱 iPhone, 💻 Windows…). If a device sends as the person who doesn't usually use it, the message gets a ⚠, and **⇄** moves it to the right person.

The web version runs in your browser. Chats are saved only in that browser, and grammar checking uses LanguageTool (spelling and basic grammar). For the free AI checker that reads the scene, download the desktop version below.
网页版直接在浏览器里用，聊天记录只存在这个浏览器里，批改只能用 LanguageTool。想用看场景的免费 AI 批改，请按下面的步骤下载电脑版。

## Quick start · 快速开始

1. Install **Node.js 18 or newer**: https://nodejs.org · 安装 Node.js（18 或更新）
2. Download this project (green **Code** button → **Download ZIP**, then unzip), or `git clone` it. · 下载本项目（Code → Download ZIP，解压）
3. Start the board · 启动：
   - **Windows**: double-click `start.bat` · 双击 `start.bat`
   - **Mac**: double-click `start.command`. The first time, Mac may block it. Right-click it → **Open** → **Open**. If it still won't run, open Terminal in this folder and run `chmod +x start.command` once.
     第一次 Mac 可能会拦截：右键 → 打开 → 打开。
   - Or, in a terminal: `node server.mjs --open`

   The board opens at http://localhost:8765. Keep the black window open while you chat. Close it to stop the board.
   浏览器会打开 http://localhost:8765。聊天时别关黑色窗口，关掉它聊天板就停止。

### Optional: free offline English checker · 可选：免费离线批改

The best free checker is a small AI model (Qwen3 4B) that runs on your own computer. It needs no internet, no subscription and no API key.
最好的免费批改是在你电脑上运行的小模型 Qwen3 4B，不要网、不要订阅、不要 API key。

```bash
node setup.mjs
```

This downloads llama.cpp's `llama-server` (about 15–40 MB) and the model (about **2.4 GB**) into the `llm/` folder. It needs about 2.8 GB of free disk space.
Then pick **🐱 本地 Qwen** in the bottom-right menu.
会下载约 2.4 GB 到 `llm/` 文件夹（需要约 2.8 GB 空间）。之后在右下角选择“🐱 本地 Qwen”。

- Windows: uses the graphics card through Vulkan (an NVIDIA card is picked automatically when there are two). Mac: uses Apple Metal.
- Each check takes about 5–30 seconds, depending on your computer. The first check also starts the model (about 10 s).
- You can use your own llama.cpp instead (for example `brew install llama.cpp`). The board looks for `llama-server` on the PATH, and the model must be in `llm/`.

## Three checkers · 三种批改引擎 (bottom-right menu · 右下角切换)

| | Checker | What it does · 说明 |
|---|---|---|
| 🐱 | **Qwen3 4B, local** | Free, works offline. Reads the chat scene, rewrites the message the way a native speaker would say it, and explains why in Chinese. Needs `node setup.mjs`. · 免费、离线，看场景改地道说法，有中文解释 |
| 🔤 | **LanguageTool** | Free, online. Checks spelling and basic grammar only. Fast, but it doesn't understand the scene. · 免费、在线，只查拼写和基本语法 |
| 🤖 | **Claude** | The most accurate. Needs your own Anthropic API key from console.anthropic.com (paste it in ⚙️ Settings). Each check costs about 1–2 US cents. · 最准，需要自己的 API key，每句约 1–2 美分 |

Every correction shows which checker made it. · 每条批改都会标明是哪个引擎改的。

## Features · 功能

- Switch the speaker with the button or Alt+S. The Chinese speaker (named S by default) is on the left; the English speaker (named A) is on the right. You can change both names in ⚙️ Settings.
- Automatic translation, line by line, so paragraphs, line breaks and lists keep their layout. In learning mode, the Chinese is blurred until you click it. Each translation has ▴ Fold (one line), ▾ Show and ✕ Hide buttons; long translations show 6 lines with "Show all". In ⚙️ Settings each device can fold or hide its own (or all) translations. Very long messages show 6 lines with "Show all".
- **中→EN** turns a Chinese draft into English. **EN→中** (for the English speaker) gives natural Chinese with pinyin and a tip.
- Red-pen corrections that read the scene: a "This moment" version, plus an "only fix mistakes" version.
- 🖼 Pictures: paste a screenshot (Ctrl+V), drag a picture onto the message box, or tap 🖼 (phone: photos or camera). Pictures are shrunk to about 100–300 KB and kept outside the chat file: in the browser, in `data/img` (desktop), and in `img/` of your ☁ sync repository so the other device can see them. Tap a picture to see it full size.
- ⭐ Vocabulary: each saved word gets a word card (phonetics, part of speech, English definitions and examples from the free dictionaryapi.dev, Chinese meaning with pinyin, the chat sentence it came from, your note) and a colour for how well you know it (New / Learning / Known). Practice shows the words you know least first, in both directions, and spaces the reviews (Forgot / Unsure / Got it). CSV export. 🔊 Read aloud. 🎤 Voice input (Chrome and Edge): it keeps listening through pauses until you tap ⏹ and tidies the text while you speak — fillers (um, you know, 嗯, 那个) and repeated words or phrases removed, changes of mind kept as meant ("周六，不对，周日" → "周日"; "at six, I mean seven" → "at seven"), phrases joined into sentences with . / ? (。/？). "↺ Original" brings back exactly what was heard.
- Message times for two places: in ⚙️ Settings each person can choose a country or region (and a time zone if it has more than one), plus an optional city. If nothing is chosen, the board uses this computer's time.
- Chats get an automatic title from what they are about (greetings skipped, in English and Chinese) and a guessed category (🍜 Food, 📅 Plans, ✈️ Travel, 🛒 Shopping, 💗 Feelings, 💼 Work & study, 🩺 Health, 🏠 Daily life). Tap the icon next to a chat, or the title at the top, to rename it (with title suggestions from the latest messages) or change the category. 🔄 next to the title (and under each chat's icon in the list) sums up the latest stretch of the chat (since the last 30-minute break) as a short title, e.g. "Flights · Hotel · Paris / 航班 · 酒店 · 巴黎" — from the words used most, or with Chrome's built-in AI when it is already installed. A title you typed yourself is never replaced without asking (Keep / Edit title / Replace); filter the list by category. 📌 pins a chat to the top; pinned chats can be dragged into any order (on a phone: hold for a moment, then drag). Other chats stay sorted by the latest message.
- Search, several conversations, Markdown export, JSON backup and restore, dark mode.

## Your data · 数据

- Chats are saved to `data/board-data.json`. There is a daily backup in `data/backups` (last 14 days).
- An API key, if you use one, is stored in `data/claude-key.txt`. It is used only by the local server and never reaches the browser.
- `data/` and `llm/` are never uploaded to git (see `.gitignore`).
- Translation: Chrome's built-in offline translator when available, otherwise the free MyMemory service. Don't type private things when using an online service.

聊天记录在 `data/` 文件夹，模型在 `llm/` 文件夹，这两个都不会上传到 GitHub。

### ☁ Sync between devices · 多设备同步 (optional)

To see the same chats on your phone and computer (web or desktop version), sync them to your own **private** GitHub repository:

1. Create a private repository, for example `bilingual-board-data`.
2. Make a [fine-grained token](https://github.com/settings/personal-access-tokens/new): under Repository access choose **Only select repositories** and pick that repository; under Permissions set **Contents** to **Read and write**.
3. In ⚙️ Settings → ☁ Sync, enter the repository (`you/bilingual-board-data`) and paste the token. Then click **Connect**. Do this once on each device.

The chats are stored as `board.json` in that repository. While someone types, a tiny `typing-A.json` / `typing-B.json` file is updated (at most every 8 s), so the other device shows "… is typing". Your own messages show ⏳ while uploading and ✓ once the other device can get them. The token is kept only in that browser. The board refuses public repositories, so your chats are never published.

想在手机和电脑上看到同样的聊天：建一个**私有**仓库，生成一把只能读写这个仓库的钥匙（fine-grained token，Contents: Read and write），在 ⚙️ 设置 → ☁ 同步 里填仓库名、粘贴钥匙、点连接。每台设备做一次。

## Files

`server.mjs` is the small local server; it has no dependencies. `index.html` is the whole app. `local.mjs` runs the free model, `claude.mjs` calls Claude, `merge.cjs` merges saved copies safely, and `setup.mjs` downloads the free model.
Pinyin comes from [pinyin-pro](https://github.com/zh-lx/pinyin-pro) (MIT), and the country/time-zone list from the IANA time zone database (public domain); both are in `vendor/`.

Settings for advanced users (environment variables): `PORT` (default 8765), `BOARD_DATA_DIR`, `LOCAL_LLM_DIR`, `LOCAL_LLM_PORT` (default 8790).

## License

Code: [PolyForm Noncommercial 1.0.0](LICENSE). Free for personal and noncommercial use. Commercial use needs written permission from skot-chen. The cat illustrations in `img/` are © skot-chen and not covered by the license.

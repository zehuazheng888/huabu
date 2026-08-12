# 化步 · NYFC 字幕生成工具

日语视频/歌曲字幕一键生成工具：**YouTube/本地文件 → 语音识别 → 双语翻译 → SRT/ASS 字幕**。

---

## 功能特性

- **语音识别**：faster-whisper large-v3（日语精度最优），支持热词、-23 LUFS 响度归一化、幻觉抑制、beam/温度/重复惩罚调优
- **双语翻译**：本地 Ollama + Qwen3（免费，无需联网 API），bilingual（日上中下）/ alternating（交替）两种布局，语速检测自动换行
- **YouTube 一键抓取**：粘贴链接 → 自动探测可用格式 → 分辨率（原画质~240p）/ 容器 / 音频 9 种格式可选 → 抓最高清封面
- **字幕样式**：6 种字幕组模板（default / ikedaCN / sugawaraCN 等），按语音间隔交替颜色便于校对
- **自动更新**：启动或点「检查更新」自动检测新版本并打开下载页
- **代码保护**：程序文件受完整性保护（防篡改 / 防倒卖），被改动会拒绝运行

---

## 下载安装

1. 下载 `NYFC_setup.zip`（约 270MB，不含模型）
2. 解压到任意目录（需要 **Windows + Python 3.14**）
3. 双击 `setup.bat` 安装依赖（一次性）
4. 双击 `启动NYFC.bat` 打开图形界面
5. **首次识别时自动从 HuggingFace 下载模型**（约 2-3GB，仅一次，之后离线可用）

> Releases 中的 `NYFC_update_*.zip` 为增量更新包（已有旧版本时下载解压覆盖即可）。

---

## 使用教程

### 图形界面
- **抓取在线视频**：粘贴 YouTube 链接 → 自动探测 → 选 分辨率/格式/音频 → 点「抓取视频」→ 点「开始识别」
- **本地文件**：点「添加文件」选音频/视频 → 点「开始识别」
- **双语翻译**：勾选「双语翻译」→ 识别后自动用本地大模型翻译成双语字幕
- **识别参数**（识别页）：模型 / 语言 / 设备 / 热词 / beam / 温度 / 重复惩罚 / 幻觉抑制 / 初始 prompt / 响度归一化
- **字幕参数**（字幕页）：字幕样式 / 拆分 / VAD / 词级时间戳 / 交替颜色
- **翻译参数**（翻译页）：翻译模型 / 双语布局 / 翻译温度 / 语速阈值 / 译文最大字符数 / 术语表
- **输出**：SRT / ASS 到输出目录（默认 `D:\NYFC_Output`，可在 config 修改）

### 命令行
```
python nyfu_oneclick.py "链接或文件" --model-size large-v3
python nyfu_oneclick.py "链接" --translate --layout alternating
python nyfu_translate.py 字幕.ass --model qwen3:8b
```

---

## 配置（config.json）

| 项 | 说明 |
|---|---|
| `model_size` / `language` / `hotwords` | 识别参数 |
| `out_dir` | 输出目录（默认 `D:\NYFC_Output`） |
| `translate_model` / `glossary` | 翻译模型 / 术语表 |
| `download_res` / `video_format` / `audio_format` | 下载格式 |
| `fetch_thumbnail` | 是否抓封面 |
| `cookies_file` | YouTube 登录态 |

---

## 常见问题

1. **抓取提示登录验证**：开代理（梯子），在浏览器登录 YouTube 后点「刷新 cookies」
2. **探测格式慢 / 失败**：需开代理，否则 yt-dlp 提取慢
3. **翻译无中文**：确认 Ollama 已启动，且已执行 `ollama pull qwen3:8b`
4. **首次识别很慢**：正在自动下载模型，完成后即正常
5. **程序被识别为改动**：代码受完整性保护，请勿自行修改程序文件；有疑问请联系作者

---

## 致谢

基于以下开源项目构建：Whisper / faster-whisper / CTranslate2 / Ollama / Qwen3 / yt-dlp / FFmpeg / pysubs2 / PyTorch 等。

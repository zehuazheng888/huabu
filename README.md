# 化步 · NYFC 字幕生成工具

日语视频/歌曲字幕一键生成工具：**YouTube/本地文件 → 语音识别 → 双语翻译 → 样式编辑 → SRT/ASS 字幕 → 封装成片**。

---

## 一键安装（推荐）

1. 下载 **`NYFC_setup_v1.2.0.zip`**（约 290MB，不含模型）并解压到任意目录
2. 双击 **`install.bat`** —— 全自动下载并安装 Python 3.14 / 依赖 / Whisper 模型 / ffmpeg（需联网，首次约 10-30 分钟）
3. 装好自动打开图形界面；之后双击 **`启动NYFC.bat`** 使用

> - 已装 Python 3.14 的用户可改双击 `setup.bat` 快速装依赖
> - 首次识别时若模型未下载，程序会自动从 HuggingFace 下载（仅一次，之后离线可用）

---

## 功能特性

- **语音识别**：faster-whisper（日语精度最优），支持热词加权（成员名/专有名词）、-23 LUFS 响度归一化、幻觉抑制、beam/温度/重复惩罚调优
- **Aegisub 风格样式管理器**：自定义字体/字号/颜色/描边/阴影/九宫格对齐/边距等，默认思源黑体50
- **双语翻译**：本地 Ollama + Qwen3（免费、无需联网 API），bilingual（日上中下）/ alternating（交替）布局，语速检测自动换行、术语表统一译名
- **封装工具**：视频 + 音频 + 字幕（软字幕）无损封装成 MKV/MP4，参考 MKVToolNix 规范（轨道语言/默认轨/强制显示）
- **YouTube 一键抓取**：粘贴链接自动探测可用格式，分辨率（原画质~240p）/ 容器 / 音频格式可选，抓最高清封面，自动读取浏览器登录态解决登录验证
- **自动更新**：启动或点「检查更新」自动检测新版本并打开下载页
- **代码保护**：程序文件受完整性保护（防篡改/防倒卖），被改动会拒绝运行

---

## 使用教程

### 图形界面
- **抓取在线视频**：粘贴 YouTube 链接 → 自动探测 → 选 分辨率/格式/音频 → 点「抓取视频」→ 点「开始识别」
- **本地文件**：点「添加文件」选音频/视频 → 点「开始识别」
- **双语翻译**：勾选「双语翻译」→ 识别后自动用本地大模型翻译成双语字幕
- **样式管理**：「字幕」页 → 点「样式管理」打开编辑器，改字体/字号/颜色后「保存」，下次识别生效
- **封装成片**：「封装」页 → 选 视频/音频/字幕 → 设输出格式 → 点「开始封装」
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

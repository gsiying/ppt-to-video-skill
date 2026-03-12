---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: a02214064a9f0c3db77ff46f52d57512
    PropagateID: a02214064a9f0c3db77ff46f52d57512
    ReservedCode1: 30450220719a063dccf99f4424ebb6a74561f9ab2a712eb9808e18de4d5148fb6525b5740221009c28ea4dbf1c24980ad10b11f2219209446246af4b8e901ac05329cf6f79f44e
    ReservedCode2: 304602210089fb0fc83fbaa38481882bf0cbe69b3cde96dd7ea01fc2687ec73aa3103d5050022100a91fb49a2dabdbdfd21f26b51ec4cef42ef9eb1e4cdaa465cc8c2092ba6ac2a9
---

# PPT 转视频配音 Skill

将 PowerPoint 演示文稿（.pptx）转换为带配音的 MP4 视频。

## 功能特性

- **自动提取备注**：从幻灯片的备注（Speaker Notes）中提取配音内容
- **智能配音生成**：使用微软 Edge TTS 生成自然流畅的女声配音
- **视频自动合成**：自动将幻灯片转换为视频并添加配音
- **灵活配置**：支持自定义语音、分辨率、帧率等参数
- **时长控制**：每个幻灯片视频时长根据内容自动调整（15-30秒）

## 环境要求

### 系统依赖

- Python 3.8+
- FFmpeg（用于视频处理）
- LibreOffice（用于 PPT 转 PDF）

### 安装系统依赖

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install -y ffmpeg libreoffice poppler-utils
```

**macOS:**
```bash
brew install ffmpeg libreoffice poppler
```

**Windows:**
下载并安装 FFmpeg、LibreOffice 和 Poppler for Windows

### 安装 Python 依赖

```bash
pip install -r requirements.txt
```

## 使用方法

### 命令行使用

```bash
python ppt_to_video_skill.py 输入文件.pptx 输出文件.mp4
```

### 高级选项

```bash
python ppt_to_video_skill.py input.pptx output.mp4 \
    --voice zh-CN-XiaoxiaoNeural \
    --rate +0% \
    --resolution 1920x1080 \
    --fps 24
```

### 参数说明

| 参数 | 默认值 | 说明 |
|------|--------|------|
| voice | zh-CN-XiaoxiaoNeural | 配音语音（女声） |
| rate | +0% | 语速（-50% 到 +100%） |
| pitch | +0Hz | 音调（-50Hz 到 +50Hz） |
| resolution | 1920x1080 | 视频分辨率 |
| fps | 24 | 视频帧率 |

### 可用语音列表

| 语音 ID | 语言 | 性别 | 风格 |
|---------|------|------|------|
| zh-CN-XiaoxiaoNeural | 中文 | 女 | 播音 |
| zh-CN-YunxiNeural | 中文 | 男 | 播音 |
| en-US-JennyNeural | 英文 | 女 | 播音 |
| en-US-GuyNeural | 英文 | 男 | 播音 |

## 在代码中使用

```python
from ppt_to_video_skill import PPTToVideoSkill

# 创建 Skill 实例（可选配置）
config = {
    "voice": "zh-CN-XiaoxiaoNeural",  # 女声
    "rate": "+0%",                    # 语速适中
    "resolution": (1920, 1080),       # 分辨率
    "fps": 24,                        # 帧率
    "min_duration": 15,               # 最小时长
    "max_duration": 30                # 最大时长
}

skill = PPTToVideoSkill(config)

# 处理 PPT 文件
result = skill.process("presentation.pptx", "output.mp4")

print(result)
# 输出示例:
# {
#     "video_path": "output.mp4",
#     "duration": 120.5,
#     "slides_count": 5,
#     "status": "success"
# }
```

## 工作流程

1. **解析 PPT**：读取 PPT 文件，提取每个幻灯片的内容和备注
2. **转换图片**：将幻灯片转换为高分辨率图片
3. **生成配音**：使用 TTS 将备注文字转换为语音
4. **合成视频**：将图片和配音合成为视频片段
5. **合并输出**：将所有片段合并为最终视频

## 注意事项

- PPT 文件中建议填写"演讲者备注"（Speaker Notes），系统会优先使用备注内容
- 如果没有备注，系统会使用幻灯片上的文字内容
- 确保 PPT 文件中的文字内容不要过多，否则配音时长可能超过 30 秒
- 建议使用 .pptx 格式的文件

## 故障排除

### 常见问题

1. **LibreOffice 转换失败**
   - 确保已正确安装 LibreOffice
   - 尝试手动转换：`libreoffice --headless --convert-to pdf yourfile.pptx`

2. **视频没有声音**
   - 检查 FFmpeg 是否正确安装
   - 确认音频编码器已启用

3. **处理速度慢**
   - 视频生成是逐个处理的，请耐心等待
   - 可以尝试降低分辨率以提高速度

## 许可证

MIT License

## 作者

MiniMax Agent

# PPT 转视频配音

将 PowerPoint 演示文稿转换为带 AI 配音的 MP4 视频。

## 功能

- 自动提取幻灯片文字内容作为配音脚本
- 使用 MiniMax TTS API 生成自然语音
- 使用 MiniMax 视频生成 API 创建视频
- 完全云端处理，无需安装额外依赖

## 使用方法

直接告诉 AI 你的需求：

```
# 基本转换
"把这个 PPT 转为视频"

# 指定风格
"用专业风格把这个 presentation.pptx 转为视频"

# 英文配音
"把 PPT 转为英文视频"
```

## 参数

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| input_file | string | 必填 | PPT 文件路径 |
| voice | string | male | 语音：male/female |
| language | string | zh | 语言：zh/en |
| style | string | professional | 风格：professional/friendly |

## 示例

```
"把 /path/to/test.pptx 转为视频"
"用女声把这份 PPT 转为带配音的视频"
"把这个 presentation 转成英文视频"
```

## 技术实现

- 配音：使用 MiniMax TTS API
- 视频：使用 MiniMax 视频生成 API
- 无需安装 FFmpeg、LibreOffice 等本地工具
- 云端自动处理

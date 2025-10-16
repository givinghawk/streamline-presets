# Streamline Presets

A collection of FFmpeg encoding presets for common media processing tasks. These presets provide optimized settings for video, audio, and image encoding across different use cases.

## 📁 Available Presets

### Video Presets
- **YouTube 1080p H.264** (`youtube-1080p-h264.json`) - Optimized for YouTube uploads at 1080p resolution
- **Archive HEVC Lossless** (`archive-hevc-lossless.json`) - Lossless archival using HEVC/H.265
- **Web VP9 Optimized** (`web-vp9-optimized.json`) - Optimized VP9 for web streaming
- **Mobile H.264 Low Bandwidth** (`mobile-h264-lowbandwidth.json`) - Mobile-friendly with reduced bitrate

### Audio Presets
- **Audio FLAC** (`audio-flac.json`) - Lossless audio compression
- **Audio Opus** (`audio-opus.json`) - Efficient audio compression for streaming

### Image Presets
- **Image WebP** (`image-webp.json`) - Modern image format with superior compression

## 📋 JSON Structure

Each preset file follows this structure:

```json
{
  "id": "unique-preset-identifier",
  "name": "Human Readable Name",
  "description": "Detailed description of what this preset does",
  "category": "video|audio|image",
  "encoder": "ffmpeg-encoder-name",
  "ffmpegArgs": [
    "-arg1", "value1",
    "-arg2", "value2"
  ]
}
```

### Field Descriptions

- **id** (string, required): Unique identifier for the preset (kebab-case recommended)
- **name** (string, required): Display name for the preset
- **description** (string, required): Detailed explanation of the preset's purpose and use case
- **category** (string, required): One of `video`, `audio`, or `image`
- **encoder** (string, required): The primary FFmpeg encoder used (e.g., `libx264`, `libvpx-vp9`)
- **ffmpegArgs** (array, required): Array of FFmpeg arguments as strings (flags and values as separate elements)

## 🚀 Usage Example

To use a preset with FFmpeg:

```bash
# Load preset
cat presets/youtube-1080p-h264.json

# Apply preset arguments to FFmpeg
ffmpeg -i input.mp4 [preset ffmpegArgs here] output.mp4
```

For example, with the YouTube 1080p preset:

```bash
ffmpeg -i input.mp4 \
  -c:v libx264 \
  -preset slow \
  -crf 18 \
  -maxrate 8M \
  -bufsize 16M \
  -vf scale=1920:1080:flags=lanczos \
  -c:a aac \
  -b:a 192k \
  -ar 48000 \
  -movflags +faststart \
  -pix_fmt yuv420p \
  output.mp4
```

## 🤝 Contributing

We welcome contributions! To add a new preset:

1. **Fork the repository**
2. **Create a new JSON file** in the `/presets` folder following the structure above
3. **Validate your JSON** - Ensure it's valid JSON syntax
4. **Test the preset** - Verify the FFmpeg arguments work correctly
5. **Submit a pull request** with:
   - Clear description of the preset's purpose
   - Use case examples
   - Any special requirements or dependencies

### Preset Guidelines

- Use descriptive, kebab-case IDs (e.g., `streaming-720p-h264`)
- Provide clear, detailed descriptions
- Include all necessary FFmpeg arguments for the complete encoding pipeline
- Optimize for the specific use case
- Document any special considerations in the description
- Ensure compatibility with recent FFmpeg versions

### Testing Your Preset

Before submitting, test your preset:

```bash
# Validate JSON syntax
python3 -m json.tool presets/your-preset.json

# Test with FFmpeg (adjust paths as needed)
ffmpeg -i test-input.mp4 [your preset args] test-output.mp4
```

## 📖 FFmpeg Resources

- [FFmpeg Official Documentation](https://ffmpeg.org/documentation.html)
- [FFmpeg Encoding Guide](https://trac.ffmpeg.org/wiki/Encode)
- [H.264 Encoding Guide](https://trac.ffmpeg.org/wiki/Encode/H.264)
- [VP9 Encoding Guide](https://trac.ffmpeg.org/wiki/Encode/VP9)
- [Audio Encoding Guide](https://trac.ffmpeg.org/wiki/Encode/HighQualityAudio)

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

Presets are based on community best practices and FFmpeg documentation.
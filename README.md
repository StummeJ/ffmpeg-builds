# FFmpeg Builds with NVIDIA CUDA Support

A comprehensive GitHub Actions workflow system for building FFmpeg on Windows x64 with full NVIDIA CUDA support. This repository provides configurable builds with various feature sets and codec options.

## Features

- **Automated FFmpeg builds** for Windows x64 using GitHub Actions
- **NVIDIA CUDA support** with configurable NVENC/CUVID acceleration
- **Multiple feature sets**: Minimal, Standard, Full, and Custom configurations
- **Configurable FFmpeg versions**: Build latest release or specific versions
- **Non-free codec support**: Optional inclusion of proprietary codecs
- **NPP integration**: NVIDIA Performance Primitives support
- **Artifact management**: Automatic upload of build artifacts and logs

## Quick Start

### Using GitHub Actions Interface

1. Navigate to the "Actions" tab in this repository
2. Select "Build FFmpeg with CUDA Support" workflow
3. Click "Run workflow"
4. Configure your build options:
   - **FFmpeg Version**: `latest` or specific version (e.g., `6.1.1`)
   - **Feature Set**: Choose from `minimal`, `standard`, `full`, or `custom`
   - **CUDA Support**: Enable/disable NVIDIA CUDA acceleration
   - **Non-free Support**: Enable proprietary codecs
   - **NPP Support**: Enable NVIDIA Performance Primitives
   - **Custom Args**: Additional configure arguments for custom builds

### Build Configurations

#### Feature Sets

- **Minimal**: Basic FFmpeg with essential codecs only
- **Standard**: Common codecs including x264, x265, and VP8/VP9
- **Full**: Complete codec suite with AV1, SVT-AV1, audio codecs, and more
- **Custom**: Use custom configure arguments for specialized builds

#### CUDA Features

When CUDA support is enabled, the following features are included:
- **NVENC**: Hardware-accelerated encoding (H.264, HEVC)
- **CUVID**: Hardware-accelerated decoding
- **NPP**: NVIDIA Performance Primitives (when enabled)
- **CUDA Toolkit 12.3**: Latest CUDA runtime and development tools

## Build System

This project uses the excellent [media-autobuild_suite](https://github.com/m-ab-s/media-autobuild_suite) scripts, which provide:

- **Comprehensive codec support**: Wide range of audio and video codecs
- **Dependency management**: Automatic handling of library dependencies
- **Optimized builds**: Performance-optimized compilation settings
- **Regular updates**: Up-to-date with latest codec versions

## Usage Examples

### Building Latest FFmpeg with Full CUDA Support

```yaml
# Workflow inputs:
ffmpeg_version: "latest"
feature_set: "full"
enable_cuda: true
enable_nonfree: false
enable_npp: false
```

### Building Specific Version with Non-free Codecs

```yaml
# Workflow inputs:
ffmpeg_version: "6.1.1"
feature_set: "full"
enable_cuda: true
enable_nonfree: true
enable_npp: true
```

### Custom Build with Specific Requirements

```yaml
# Workflow inputs:
ffmpeg_version: "latest"
feature_set: "custom"
enable_cuda: true
enable_nonfree: false
enable_npp: false
custom_configure_args: "--enable-libass --enable-libfreetype --disable-debug"
```

## Build Artifacts

After a successful build, the following artifacts are available for download:

### FFmpeg Build Artifacts
- **ffmpeg.exe**: Main FFmpeg executable with all configured features
- **ffprobe.exe**: Media analysis and information tool
- **ffplay.exe**: Simple media player for testing
- **build-info.txt**: Detailed build configuration and environment info

### Build Logs
- Complete build logs for troubleshooting
- Configuration files used during build
- Error logs if build fails

## NVIDIA CUDA Requirements

### For Building
- No special requirements - CUDA toolkit is automatically installed during build

### For Runtime
To use the built FFmpeg with CUDA acceleration:
- NVIDIA GPU with Compute Capability 3.0+
- NVIDIA driver 520.61 or newer
- CUDA runtime libraries (typically included with recent NVIDIA drivers)

### Verifying CUDA Support

After downloading the built FFmpeg, verify CUDA support:

```cmd
ffmpeg -hwaccels
```

Should show:
```
Hardware acceleration methods:
cuda
cuvid
nvdec
nvenc
```

## Supported Codecs and Libraries

### Video Codecs
- **x264**: H.264/AVC encoder
- **x265**: HEVC/H.265 encoder  
- **AV1**: AOM AV1 encoder/decoder
- **SVT-AV1**: Scalable Video Technology AV1
- **VP8/VP9**: WebM video codecs
- **DAV1D**: Fast AV1 decoder
- **Theora**: Ogg Theora codec

### Audio Codecs
- **MP3 LAME**: High-quality MP3 encoder
- **Opus**: Modern audio codec
- **Vorbis**: Ogg Vorbis codec
- **FDK-AAC**: High-quality AAC encoder (when non-free enabled)

### Hardware Acceleration
- **NVENC**: NVIDIA hardware encoding
- **CUVID**: NVIDIA hardware decoding  
- **NVDEC**: NVIDIA video decode API
- **NPP**: NVIDIA Performance Primitives

## Workflow Configuration

The build workflow can be triggered by:

- **Manual dispatch**: Using the GitHub Actions interface
- **Push events**: Automatic builds on push to main/master branches
- **Pull requests**: Build verification for PRs

### Environment Variables

- `BUILD_TYPE`: Set to "Release" for optimized builds
- `CUDA_VERSION`: CUDA toolkit version (currently 12.3)

## Troubleshooting

### Common Issues

1. **Build timeout**: Increase `timeout-minutes` in workflow if needed
2. **CUDA installation fails**: Check CUDA version compatibility
3. **Missing codecs**: Verify feature set selection and non-free options
4. **Build logs**: Always check uploaded build logs for detailed error info

### Getting Help

- Check the [Issues](../../issues) section for known problems
- Review build logs in the Actions tab
- Consult the [media-autobuild_suite documentation](https://github.com/m-ab-s/media-autobuild_suite)

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Test your changes thoroughly
4. Submit a pull request with detailed description

## License

This project configuration is released under the MIT License. Note that:
- FFmpeg itself has its own licensing terms
- Some codecs require separate licensing for commercial use
- Non-free components have additional restrictions

## Acknowledgments

- [media-autobuild_suite](https://github.com/m-ab-s/media-autobuild_suite) for the excellent build scripts
- NVIDIA for CUDA toolkit and hardware acceleration APIs
- FFmpeg project and all codec developers
- GitHub Actions for the CI/CD infrastructure
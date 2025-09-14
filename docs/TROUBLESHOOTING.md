# FFmpeg Build Troubleshooting Guide

This guide helps resolve common issues when building FFmpeg with CUDA support.

## Common Build Issues

### 1. Build Timeout
**Problem**: Workflow times out during the build process.

**Solution**: 
- Increase `timeout-minutes` in the workflow file
- Use a more minimal feature set for faster builds
- Check if the build is stuck on a specific component

### 2. CUDA Installation Failure
**Problem**: CUDA toolkit installation fails.

**Symptoms**:
```
Error: Failed to install CUDA toolkit
CUDA_PATH not found
```

**Solutions**:
- Check CUDA version compatibility with Windows runner
- Verify CUDA download URL is accessible
- Try a different CUDA version in the workflow environment

### 3. Missing Codecs in Final Build
**Problem**: Expected codecs are not available in the built FFmpeg.

**Diagnosis**:
```cmd
ffmpeg -codecs | grep [codec_name]
ffmpeg -encoders | grep [encoder_name]
```

**Solutions**:
- Verify feature set selection includes desired codecs
- Check if non-free codecs require `enable_nonfree: true`
- Review build configuration in the logs
- Ensure dependencies were built successfully

### 4. Hardware Acceleration Not Available
**Problem**: NVENC/CUVID not working in built FFmpeg.

**Diagnosis**:
```cmd
ffmpeg -hwaccels
ffmpeg -encoders | grep nvenc
ffmpeg -decoders | grep cuvid
```

**Solutions**:
- Ensure `enable_cuda: true` was set
- Verify CUDA toolkit installation succeeded
- Check build logs for NVENC/CUVID compilation errors
- Confirm target machine has compatible NVIDIA GPU and drivers

### 5. Build Artifacts Missing
**Problem**: No artifacts uploaded or downloaded.

**Solutions**:
- Check if build completed successfully
- Review artifact upload step logs
- Verify artifact paths in workflow configuration
- Look for FFmpeg executables in alternative locations

## Debugging Steps

### 1. Check Build Logs
Always start by examining the build logs:
1. Go to Actions → Failed workflow run
2. Expand "Run media-autobuild_suite" step
3. Look for error messages and failed components
4. Download "build-logs" artifact for detailed analysis

### 2. Verify Environment Setup
Check environment setup steps:
- MSYS2 installation and package updates
- CUDA toolkit download and installation
- Environment variables and PATH setup

### 3. Configuration Review
Examine the generated build configuration:
- Review "Configure Build Options" step output
- Verify feature set mappings are correct
- Check custom configure arguments syntax

### 4. Component-Specific Issues

#### x264/x265 Build Failures
- Often related to assembly compilation
- Check NASM/YASM availability
- Review compiler flags and optimization levels

#### CUDA-Related Failures
- Verify CUDA toolkit version compatibility
- Check NVIDIA driver requirements
- Confirm GPU Compute Capability support

#### Audio Codec Issues
- Check dependency library availability
- Verify licensing compatibility
- Review feature set configuration

## Performance Optimization

### Build Time Reduction
1. **Use Minimal Feature Set**: Start with minimal builds for testing
2. **Disable Unnecessary Components**: Remove unused codecs and libraries
3. **Parallel Building**: Ensure make is using multiple cores
4. **Source Caching**: Consider caching downloaded sources

### Runtime Performance
1. **Hardware Acceleration**: Always enable CUDA when available
2. **Optimization Flags**: Use release builds with optimization
3. **Threading**: Configure appropriate thread counts
4. **Memory Management**: Monitor memory usage during encoding

## Version-Specific Issues

### FFmpeg Version Problems
- **Latest**: May have unstable or experimental features
- **Specific Versions**: Check version compatibility with codecs
- **LTS Versions**: Consider using stable LTS releases

### CUDA Version Compatibility
| CUDA Version | Min Driver | Supported GPUs |
|--------------|------------|----------------|
| 12.3         | 546.01     | All GTX 10xx+ |
| 11.8         | 522.06     | All GTX 10xx+ |
| 11.0         | 451.22     | All GTX 10xx+ |

## Getting Additional Help

### Log Analysis
When reporting issues, include:
- Complete workflow run URL
- Specific error messages
- Build configuration used
- Expected vs actual behavior

### Resources
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)
- [NVIDIA Video Codec SDK](https://developer.nvidia.com/nvidia-video-codec-sdk)
- [media-autobuild_suite Issues](https://github.com/m-ab-s/media-autobuild_suite/issues)

### Community Support
- [FFmpeg Users Mailing List](https://lists.ffmpeg.org/mailman/listinfo/ffmpeg-user)
- [NVIDIA Developer Forums](https://forums.developer.nvidia.com/)
- [GitHub Issues](../../issues) for workflow-specific problems
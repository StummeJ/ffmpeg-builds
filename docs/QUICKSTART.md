# Quick Start Examples

This file contains practical examples for getting started with the FFmpeg build system.

## Basic Usage Examples

### 1. Gaming/Streaming Build
For OBS Studio and game recording:
```
Go to: Actions → Build FFmpeg with CUDA Support → Run workflow
Configure:
- FFmpeg Version: latest
- Feature Set: standard  
- Enable CUDA: ✓
- Enable Non-free: ✗
- Enable NPP: ✗
- Custom Args: (leave blank)
```

### 2. Content Creator Build  
For YouTube creators and professional video editing:
```
Go to: Actions → Build FFmpeg with CUDA Support → Run workflow
Configure:
- FFmpeg Version: latest
- Feature Set: full
- Enable CUDA: ✓ 
- Enable Non-free: ✓
- Enable NPP: ✓
- Custom Args: (leave blank)
```

### 3. Server/Automation Build
For server-side processing and Docker containers:
```
Go to: Actions → Build FFmpeg with CUDA Support → Run workflow  
Configure:
- FFmpeg Version: latest
- Feature Set: minimal
- Enable CUDA: ✗
- Enable Non-free: ✗
- Enable NPP: ✗
- Custom Args: --disable-programs --enable-small
```

### 4. Development Build
For FFmpeg development and testing:
```
Go to: Actions → Build FFmpeg with CUDA Support → Run workflow
Configure:
- FFmpeg Version: latest
- Feature Set: custom
- Enable CUDA: ✓
- Enable Non-free: ✗  
- Enable NPP: ✗
- Custom Args: --enable-debug --extra-cflags=-g
```

## Build Time Estimates

- **Minimal**: ~30-45 minutes
- **Standard**: ~60-90 minutes  
- **Full**: ~120-180 minutes
- **Full + Non-free**: ~150-240 minutes

## Verifying Your Build

After downloading the artifacts:

1. **Check FFmpeg version**:
   ```cmd
   ffmpeg.exe -version
   ```

2. **Verify CUDA support** (if enabled):
   ```cmd
   ffmpeg.exe -hwaccels
   ```
   Should show: `cuda`, `cuvid`, `nvdec`, `nvenc`

3. **List available encoders**:
   ```cmd  
   ffmpeg.exe -encoders | findstr nvenc
   ```

4. **Test CUDA encoding**:
   ```cmd
   ffmpeg.exe -f lavfi -i testsrc=duration=10:size=1920x1080:rate=30 -c:v h264_nvenc test_cuda.mp4
   ```

## Common Use Cases

### Encode with NVENC
```cmd
ffmpeg.exe -i input.mp4 -c:v h264_nvenc -preset medium -b:v 5M output.mp4
```

### Stream to Twitch with NVENC  
```cmd
ffmpeg.exe -f dshow -i video="Your Camera" -c:v h264_nvenc -preset llhq -b:v 3000k -maxrate 3000k -bufsize 6000k -f flv rtmp://live.twitch.tv/live/YOUR_STREAM_KEY
```

### Batch Convert with Hardware Acceleration
```cmd
for %%f in (*.mp4) do ffmpeg.exe -hwaccel cuda -i "%%f" -c:v h264_nvenc -preset medium "converted_%%f"
```

## Need Help?

- Check [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) for common issues
- Review build logs in the Actions tab if builds fail
- Use configuration templates in `configs/templates/` for proven settings
# FFmpeg Build Configuration Templates

This directory contains pre-configured build templates for common use cases.

## Available Templates

### gaming-streamer.yml
Configuration optimized for game streaming and recording with NVENC support.

### content-creator.yml  
Full-featured build for video content creators with all major codecs.

### minimal-server.yml
Lightweight build for server environments with essential codecs only.

### research-dev.yml
Development build with debugging symbols and additional tools.

## Usage

Copy the desired template configuration and customize the workflow dispatch inputs accordingly.

Example using the gaming streamer template:
1. Go to Actions → Build FFmpeg with CUDA Support → Run workflow
2. Use the parameters specified in `gaming-streamer.yml`
---
title: "How to build FAT FFmpeg"
date: 2020-08-02 18:00:00
categories: ffmpeg
---

# How to make FAT ffmpeg static library
1. Download ffmpeg library
2. Download gas-preprocessor.pl
   1. (https://github.com/hankyojeong/gas-preprocessor)
   2. I attached gas-preprocessor.pl
3. Make 'bin' directory in ffmpeg root path
4. Copy 'gas-preprocessor.pl' to {ffmpeg root path}/bin directory
5. git clone the ios-build-ffmpeg script in {ffmpeg root path}
   1. (https://github.com/hankyojeong/FFmpeg-iOS-build-script)
6. Execute "$ ./build-ffmpeg.sh"

## How to check CPU type in static library
$ lipo -info [library name]
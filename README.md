# gstreamer-learn

## 一、gstreamer初体验
### 下载
```shell
git clone https://gitlab.freedesktop.org/gstreamer/gstreamer.git
```
### 安装meson
```shell
sudo apt-get install meson
meson -v

# 升级meson版本
sudo apt-get install python3-pip
pip3 install meson==0.63
```

### 构建
```shell
cd gstreamer
meson build

cd build
ninja
sudo ninja install
```

### 配置
```shell
meson --reconfigure -Dlibav=enabled -Dgst-plugins-ugly:x264=enabled -Dgpl=enabled build
```

### 进入开发环境（development environment）
```shell
./gst-env.py
```

### 测试
```shell
which gst-launch-1.0

# 播放测试视频
gst-launch-1.0 videotestsrc ! autovideosink

# 播放在线视频
gst-launch-1.0 playbin uri=https://gstreamer.freedesktop.org/data/media/sintel_trailer-480p.webm

# 播放本地视频
gst-launch-1.0 playbin uri=file:///home/lorien/work/media/test.mp4
```

### VSCode 调试
编译可调式程序
```shell
./gst-env.sh

gcc -g basic-tutorial-3.c -o basic-tutorial-3 `pkg-config --cflags --libs gstreamer-1.0`
```

配置launch.json
```shell
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "GStreamer - Build and debug",
      "request": "launch",
      "type": "cppdbg",
      "linux": {
        "MIMode": "gdb"
      },
      "program": "/work2/media/gstreamer/subprojects/gst-docs/examples/tutorials/basic-tutorial-3",
      "cwd": "/work2/media/gstreamer/subprojects/gst-docs/examples/tutorials/",
      "stopAtEntry": false,
    }
  ]
}
```

# RTSP Video Streaming

## Prerequisites

- Ubuntu 16.04
- GCC (gcc and g++) ver. 5.4
- USB camera (v4l2 compatible)

## Getting Started

Clone the repository:

```bash
git clone https://github.com/ramilsafnab1996/rtsp-video-server.git

git submodule update --init

cd rtsp-video-server
```

### Dependencies

Install the dependencies (using `apt` package manager):

```bash
sudo apt-get install liblog4cpp5-dev
```

Install the dependencies from the `contrib`:

```bash
cd contrib

# Live555 video streaming server framework
cd live && ./genMakefiles linux-64bit && make -j$(nproc)

cd ../..
```

The most time- and nerve-consuming part, installing FFMpeg ...:

`cd` into the `scripts` directory (prepared bash scripts for installation):

```bash
cd scripts && chmod +x *

./install_ffmpeg_with_deps.sh

cd ..
```

### Build

```bash
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=RELEASE ..
make -j$(nproc)
```

### Run

Edit [`config.yaml`](config.yaml) for your needs.

Then you can run the server:

``` bash
./video_server ../config.yaml
```

## Testing
For simple testing whether the server works or not you can use MPlayer (preferred) or VLC:
```bash
sudo apt install mplayer

mplayer -benchmark rtsp://<ip address>:8554/webcam_0
```

## Limitations

- Currently there is no support for the already compressed raw camera formats (e.g. MJPEG). In this case we have 2 options: send the data as it is (e.g. MJPEG stream) or transcode the original video stream into the format we need (e.g. H.264). 
- Lack of control of camera parameters (fps, resolution, etc.) at runtime (no API for that is provided).
- RTSP multicast broadcasting is not supported (It can be implemted using Live555 API).
- SSL is not supported (see SRTP).






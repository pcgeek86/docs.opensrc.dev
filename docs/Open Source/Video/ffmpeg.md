# FFmpeg Open Source CLI

FFmpeg is a powerful command line interface (CLI) that handles audio and video processing tasks.
I like to think of FFmpeg as a "Swiss army knife" for media processing, due to its wide range of capabilities.

### FFmpeg Use Cases

* Record your desktop
* Convert between different file formats (eg `mkv` to `mp4`)
* Capture Real-Time Streaming Protocol (RTSP) streams from security cameras and record to disk
* Resize video resolution and bitrate

### Resize Video Resolution

To change the resolution of a video, using FFmpeg, use the `scale` video filter.
There are several different scale filters, in fact, but the most basic one is simply called `scale`.
The `-vf` parameter is used to apply a filter to an input video stream.
The `-y` parameter simply allows overwriting of the destination file, if it already exists.

```
ffmpeg -y -i source.mp4 -vf scale=width=1280:height=720 output.mp4
```

### Crop Video

Sometimes you only care about a certain section of video, from a camera stream.
This is especially true for security cameras, where the wide lens angle can capture a wider area than is necessary to monitor specific items.
You can use the `crop` video filter to crop the contents of a video.

If you specify the `x` and `y` parameters, without specifying the `w` (width) and `h` (height) parameters, the filter will fail to operate.
FFmpeg will ignore the filter but continue to process other valid filters.

```
ffmpeg -y -i source.mp4 -vf crop=x=1500:y=800:w=500:h=300 -t 5 output.mkv
```

| Parameter | Description                            |
| --------- | -------------------------------------- |
| w         | The width of the video to capture      |
| h         | The height of the video to capture     |
| x         | The left starting edge to capture from |
| y         | The top starting edge to capture from  |


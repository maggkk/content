---
title: DASH Adaptive Streaming for HTML video
slug: Web/API/Media_Source_Extensions_API/DASH_Adaptive_Streaming
page-type: guide
---

{{DefaultAPISidebar("Media Source Extensions")}}

Dynamic Adaptive Streaming over HTTP (DASH) is an adaptive streaming protocol. This means that it allows for a video stream to switch between bit rates on the basis of network performance, in order to keep a video playing.

First you'll need to convert your WebM video to a DASH manifest with the accompanying video files in various bit rates. To start with you'll only need the FFmpeg program from [ffmpeg.org](https://www.ffmpeg.org/), with libvpx and libvorbis support for WebM video and audio, at least version 2.5 (probably; this was tested with 3.2.5).

First, use your existing WebM file to create one audio file and multiple video files. In the example below, the file **_in.video_** can be any container with at least one audio and one video stream that can be decoded by FFmpeg.

Create the audio using:

```bash
ffmpeg -i in.video -vn -acodec libvorbis -ab 128k -dash 1 my_audio.webm
```

Create each video variant.

```bash
ffmpeg -i in.video -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1 -f webm -dash 1 \
-an -vf scale=160:90 -b:v 250k -dash 1 video_160x90_250k.webm
```

```bash
ffmpeg -i in.video -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1  -f webm -dash 1 \
-an -vf scale=320:180 -b:v 500k -dash 1 video_320x180_500k.webm
```

```bash
ffmpeg -i in.video -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1  -f webm -dash 1 \
-an -vf scale=640:360 -b:v 750k -dash 1 video_640x360_750k.webm
```

```bash
ffmpeg -i in.video -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1  -f webm -dash 1 \
-an -vf scale=640:360 -b:v 1000k -dash 1 video_640x360_1000k.webm
```

```bash
ffmpeg -i in.video -c:v libvpx-vp9 -keyint_min 150 -g 150 -tile-columns 4 -frame-parallel 1  -f webm -dash 1 \
-an -vf scale=1280:720 -b:v 1500k -dash 1 video_1280x720_1500k.webm
```

Or do it in all in one command.

```bash
ffmpeg -i in.video -c:v libvpx-vp9 -keyint_min 150 \
-g 150 -tile-columns 4 -frame-parallel 1 -f webm -dash 1 \
-an -vf scale=160:90 -b:v 250k -dash 1 video_160x90_250k.webm \
-an -vf scale=320:180 -b:v 500k -dash 1 video_320x180_500k.webm \
-an -vf scale=640:360 -b:v 750k -dash 1 video_640x360_750k.webm \
-an -vf scale=640:360 -b:v 1000k -dash 1 video_640x360_1000k.webm \
-an -vf scale=1280:720 -b:v 1500k -dash 1 video_1280x720_1500k.webm
```

Then, create the manifest file.

```bash
ffmpeg \
  -f webm_dash_manifest -i video_160x90_250k.webm \
  -f webm_dash_manifest -i video_320x180_500k.webm \
  -f webm_dash_manifest -i video_640x360_750k.webm \
  -f webm_dash_manifest -i video_1280x720_1500k.webm \
  -f webm_dash_manifest -i my_audio.webm \
  -c copy \
  -map 0 -map 1 -map 2 -map 3 -map 4 \
  -f webm_dash_manifest \
  -adaptation_sets "id=0,streams=0,1,2,3 id=1,streams=4" \
  my_video_manifest.mpd
```

The `-map` arguments correspond to the input files in the sequence they are given; you should have one for each file. The `-adaptation_sets` argument assigns them into adaptation sets; for example, this creates one set (0) that contains the streams 0, 1, 2 and 3 (the videos), and another set (1) that contains only stream 4, the audio stream.

Put the manifest and the associated video files on your web server or CDN. DASH works via HTTP, so as long as your HTTP server supports byte range requests, and it's set up to serve `.mpd` files with `Content-Type: application/dash+xml`, then you're all set.

Then, in order to correctly connect this `.mpd` file to your `<video>` element, you need a JavaScript library like dash.js, because no browser has native support for DASH. Read [dash.js quickstart](https://dashif.org/dash.js/pages/quickstart/) for how to set up your page to use it.

## See also

- [WebM DASH Specification at The WebM Project](https://wiki.webmproject.org/adaptive-streaming/webm-dash-specification)
- [DASH Industry Forum](https://dashif.org/)
- [WebM project description of how to create DASH files with FFMPEG](https://wiki.webmproject.org/adaptive-streaming/instructions-to-playback-adaptive-webm-using-dash)

# How To Record your Screen with ffmpeg

## Dependency Install

`apt-get install ffmpeg`

## Record

```
ffmpeg -y -video_size 1920x1080 -framerate 10 -f x11grab -i :0 -f pulse -ac 2 -i default screen1_recording_`date '+%Y-%m-%d_%H-%M-%S'`.mp4
```

# How To Streaming a Local Camera into RTSP

## How To

`/usr/bin/cvlc -vvv v4l2:///dev/video0 --sout '#transcode{vcodec=mp4v,vb=5000,acodec=none}:rtp{sdp=rtsp://:8554/}'`

Where `8554` is your RTSP port and `/dev/video0` is your local camera device.

## Register as systemd service

```
$ systemctl cat rtsp-cam.service
# /etc/systemd/system/rtsp-cam.service
[Unit]
Description=Camera RTSP Streaming Service
After=network-online.target
Before=homeassistant.target

[Service]
Type=simple
User=homeassistant
Restart=on-failure
CPUAffinity=3
RestartSec=120
ExecStart=/usr/bin/cvlc -vvv v4l2:///dev/video0 --sout '#transcode{vcodec=mp4v,vb=5000,acodec=none}:rtp{sdp=rtsp://:8554/}'

[Install]
WantedBy=multi-user.target

```

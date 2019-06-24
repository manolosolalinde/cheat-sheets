# Useful commands

Cut from video \
`ffmpeg -ss 00:01:28 -t 00:01:54 -i soccer_game.mp4 -acodec copy -vcodec copy -async 1 cut2.mp4`

Get video information \
`ffmpeg -i cut2.mp4`

Turn .h264 to .mp4 \
```bash
ffmpeg -loglevel info -f h264 -y -i filename.h264 -vcodec copy -r 25 newfilename
```

## Mix videos in one
ffmpeg -i out-2019_06_24_011838rp1.mp4 -i out-2019_06_24_011838rp2.mp4 -c:v h264_omx -filter_complex hstack output5.mp4


```bash
ffmpeg \
  -i out-2019_06_24_011838rp1.mp4 \
  -i out-2019_06_24_011838rp2.mp4 \
  -filter_complex '[0:v]pad=iw*2:ih[int];[int][1:v]overlay=W/2:0[vid]' \
  -map [vid] \
  -c:v h264 \
  -crf 23 \
  -preset veryfast \
  output.mp4

  ffmpeg \
  -i out-2019_06_24_011838rp1.mp4 \
  -i out-2019_06_24_011838rp2.mp4 \
  -filter_complex '[0:v]pad=iw*2:ih[int];[int][1:v]overlay=W/2:0[vid]' \
  -map [vid] \
  -c:v libx264 \
  output2.mp4
  ```

con audios \
```bash
ffmpeg -i out-2019_06_24_011838rp1.mp4 -i out-2019_06_24_011838rp2.mp4 -filter_complex \
"[0:v][1:v]hstack=inputs=2[v]; \
 [0:a][1:a]amerge[a]" \
-map "[v]" -map "[a]" -ac 2 output3.mp4
```

sin audios Nota: corre a 0.17x en raspberry 1.14x en mi compu \
```bash
ffmpeg -i out-2019_06_24_011838rp1.mp4 -i out-2019_06_24_011838rp2.mp4 -filter_complex \
"[0:v][1:v]hstack=inputs=2[v]" \
-map "[v]" -ac 2 output4.mp4
```
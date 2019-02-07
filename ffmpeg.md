# Useful commands

Cut from video \
`ffmpeg -ss 00:01:28 -t 00:01:54 -i soccer_game.mp4 -acodec copy -vcodec copy -async 1 cut2.mp4`

Get video information \
`ffmpeg -i cut2.mp4`


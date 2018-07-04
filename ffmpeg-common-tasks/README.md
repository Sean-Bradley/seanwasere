# FFMPEG Common Tasks

## Split video into smaller segments

`ffmpeg -i input.mp4 -acodec copy -f segment -segment_time 60 -vcodec copy -reset_timestamps 1 -map 0 -an output%d.mp4`

Note that the %d in your output segments are replaced by a sequence number.

## Convert FLV to MP4

`ffmpeg -i input.flv -codec copy output.mp4`

## Adjust audio levels in video

Set to DB

`ffmpeg -i inputfile -vcodec copy -af "volume=-3dB" outputfile`

or adjust by percent. 0.5 = half volume, 2.0 = double volume.

`ffmpeg -i inputfile -vcodec copy -af "volume=0.5" outputfile`

Using highpass and lowpass

`ffmpeg -i inputfile -vcodec copy -af "volume=1.5, highpass=f=500, lowpass=f=5000" outputfile`

## Convert mp4 to gif

`ffmpeg -i input.mp4 output.gif`

## Crop Video

`ffmpeg -i in.mp4 -filter:v "crop=out_w:out_h:x:y" out.mp4`

## De-interlace video

`ffmpeg -i input.mp4 -vf yadif=1 -acodec ac3 -ab 192k -vcodec mpeg4 -f mp4 -y -qscale 0 output.mp4`

## Extract a frame from a video

`ffmpeg -ss 1 -i vid.MTS -qscale:v 0 output.jpg`

## Extract multiple frames at a certain frames per second

`ffmpeg -ss 1 -i input.MOV -vf fps=5 -qscale:v 0 output%05d.jpg`




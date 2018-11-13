# videoconvert
A ffmpeg wrapper to drive it for video conversion, without dealing with the complicated command line interface.

# Introduction
Particularity of this wrapper is that it is independent on any external library; you only need "out of the box" python stuff.
It is a wrapper around the `ffmpeg` tool that rescale and change bitrate of a video file mapping a clean and easy command line interface to the `ffmpeg`'s complex one.

The current capabilities of the tool at the moment are limited to rescale and change bitrate of a video, and remove audio track.
# Installation
Ensure you have `python` and `git` installed on your system, then
```
git clone https://github.com/alvise72/videoconvert.git
cp videconvert/video-convert /usr/local/bin
```
# Usage
## Command line options
```
$ video-convert -h
Usage: video-convert [OPTIONS] <filename> [OPTIONS]

Options:
  -h, --help            show this help message and exit
  -b BITRATE, --bitrate=BITRATE
                        Set the new bitrate (can be an pure number or a number
                        followed by 'k', 'K', 'm', 'M') or a percentage
  -s SCALE, --scale=SCALE
                        Specifies the scale ratio for the resolution; can be a
                        floating number greater than 0 and less or equal to 1,
                        or an integer between 1 and 100 followed by '%'
  -a, --remove-audio    Remove autio track
  -v, --verbose         Prints out useful debug information
  -i, --info            Prints out size and bitrate of the video
  -O, --overwrite       Overwrite output file if already exists
  -P FFMPEG, --ffmpeg-path=FFMPEG
                        Alternative path of ffmpeg binary
  -p FFPROBE, --ffprobe-path=FFPROBE
                        Alternative path of ffprobe binary
  -o OUTFILE, --output-file=OUTFILE
                        Alternative path for output file
```
## Typical jobs
### Just get video information
```
$ video-convert -i ~/Video/video.mp4                                
Height: 720, Width: 1280, bitrate: 11621115
```
### Rescale video of a certain percentage
```
$ video-convert --scale 50% ~/Desktop/video.mp4 --output-file ~/Desktop/video-rescaled.mp4
Finished conversion. Output file is /Users/dorigo_a/Desktop/video-rescaled.mp4
Conversion time millis: 149419, 4472293.00 bytes/s
```
Previous conversion reduced height and width by 50%, which means that the total resolution (total number of pixels) has been reduced to 1/4. Bitrate is automatically reduced by `ffmpeg`.

### Reduce quality
```
$ video-convert --bitrate 256k ~/Desktop/video.mp4 -o ~/Desktop/video-lowquality.mp4
Finished conversion. Output file is /Users/dorigo_a/Desktop/video-rescaled.mp4
Conversion time millis: 142696, 4683001.00 bytes/s
```
In this example bitrate is reduced from 11621115 bytes/s (11.08 MBytes/s) to 262144 bytes/s (256 kBytes/s).

Bitrate cannot be increased above the original value (that one printed using `--info` option).

Of course in this case quality reduction without a rescaling leads to a more grany movie.

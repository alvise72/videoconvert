# videoconvert
A ffmpeg wrapper to drive it for video conversion, without dealing with the complicated command line interface.

# Introduction
Particularity of this wrapper is that it is independent on any external library; you only need "out of the box" python stuff.
It is a wrapper around the `ffmpeg` tool that rescale and change bitrate of a video file mapping a clean and easy command line interface to the `ffmpeg`'s complex one.

The current capabilities of the tool at the moment are limited to rescale and change bitrate of a video, and remove audio track.
# Installation
Ensure you have `python` and `git` installed on your system, then
```
git clone
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
## Tipical jobs
### Just get video information
```
$ video-convert -i ~/Video/video.mp4                                
Height: 720, Width: 1280, bitrate: 11621115
```
### Rescale video of a certain percentage
```
$ video-convert -s 50% ~/Desktop/video.mp4 -o ~/Desktop/video-rescaled.mp4 -O
Specified zero bitrate or not specified at all. Resetting it to the original value 11621115.
```

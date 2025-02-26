# video-compare

[![GitHub release](https://img.shields.io/github/release/pixop/video-compare)](https://github.com/pixop/video-compare/releases)

Split screen video comparison tool written in C++14 using FFmpeg libraries and SDL2.

`video-compare` can be used to visually compare e.g. the effect of codecs and resizing algorithms on
two video files played in sync. The tool is not very restrictive as videos are not required to be the
same resolution, color format, container format, codec or duration. However, for the best result video
files should have the same frame rate.

A movable slider enables easy viewing of the difference across any region of interest.

Thanks to the versatility of FFmpeg, it is actually also possible to use `video-compare` to compare
two images. The common PNG and JPEG formats have been successfully tested to work.

## Installation

Install [via Homebrew](https://formulae.brew.sh/formula/video-compare):

```
brew install video-compare
```

Or [build it yourself](#build).

## Screenshots

Visual compare mode:
![Visual compare mode](screenshot_1.jpg?raw=true)

Subtraction mode (and zoom activated):
![Subtraction mode"](screenshot_2.jpg?raw=true)

## Credits

`video-compare` was created by Jon Frydensbjerg (email: jon@pixop.com). The code is mainly based on
the excellent video player GitHub project: https://github.com/pockethook/player

Many thanks to the [FFmpeg](https://github.com/FFmpeg/FFmpeg), [SDL2](https://github.com/libsdl-org/SDL) and [stb](https://github.com/nothings/stb) authors.

## Usage

Launch in disallow high DPI mode. Video pixels become doubled on high DPI displays. Recommended
for displaying HD 1080p video on e.g. a Retina 5K display:

    ./video-compare video1.mp4 video2.mp4

Allow high DPI mode on systems which supports that. Video pixels are displayed "1-to-1". Useful
for e.g. displaying UHD 4K video on a Retina 5K display:

    ./video-compare -d video1.mp4 video2.mp4

Use a specific window size instead of deriving the window size from the video dimensions. The video
frame will be scaled to fit. If either width or height is left out, the missing value will be calculated
from the other specified dimension so that aspect ratio is maintained. Useful for downscaling high resolution
video onto a low resolution display:

    ./video-compare -w 1280x720 video1.mp4 video2.mp4

Shift the presentation time stamps of the right video instead of assuming the videos are aligned. A
positive amount has the effect of delaying the left video while negative values conversely delays the
right video. Useful when videos are slightly out of sync:

    ./video-compare -t 80 video1.mp4 video2.mp4

Display videos stacked vertically at full size without a slider (`hstack` for horizontal stacking is
also supported):

    ./video-compare -m vstack video1.mp4 video2.mp4

The above arguments can be combined in any order, of course.

## Controls

- Space: Toggle play/pause
- Escape: Quit
- Down arrow: Seek 15 seconds backward
- Left arrow: Seek 1 second backward
- Page down: Seek 600 seconds backward
- Up arrow: Seek 15 seconds forward
- Right arrow: Seek 1 second forward
- Page up: Seek 600 seconds forward
- S: Swap left and right video
- A: Previous frame
- D: Next frame
- F: Save both frames as PNG images in the current directory
- Z: Zoom area around cursor (result shown in lower left corner)
- C: Zoom area around cursor (result shown in lower right corner)
- 1: Toggle hide/show left video
- 2: Toggle hide/show right video
- 3: Toggle hide/show HUD
- 0: Toggle video/subtraction mode
- +: Time-shift right video 1 frame forward
- -: Time-shift right video 1 frame backward

Move the mouse horizontally to adjust the movable slider position. Click the mouse to perform a time
seek based on the horizontal position of the slider relative to the window width.

## Requirements

Requires FFmpeg headers and development libraries to be installed, along with SDL2
and its TrueType font rendering add on (libsdl2_ttf).

On Debian GNU/Linux the required development packages can be installed via `apt`:

```sh
apt install libavformat-dev libswscale-dev libsdl2-dev libsdl2-ttf-dev
```

For macOS, these dependencies can be installed with [Homebrew](https://brew.sh/):

```sh
brew install ffmpeg sdl2 sdl2_ttf
```

<small>`video-compare` will hopefully be [added to Homebrew in the future](https://github.com/pixop/video-compare/issues/1).</small>

## Build

Compile the source code:

    make

The linked `video-compare` executable will be created in the soure code directory. To perform a system wide installation:

    make install

Note that root privileges are required to perform this operation in most environments (hint: use e.g. `sudo`).

## Notes

1. Audio playback is not supported.

2. Pre-built Windows 10 64-bit releases are available from this page (simply extract the
   .zip-archive and run `video-compare.exe` from a command prompt).

## Practical tips

### Send To integration in Windows File Explorer

You can fire up the tool directly from the File Explorer when you don't need to specify
any other arguments than the inputs via Right click -> Send To -> video-compare.

Here is how this integration works:

https://user-images.githubusercontent.com/8549626/166630445-c8c511b7-005f-48aa-83bc-0eb9676cfa2a.mp4

You can do that quickly by selecting two files, then right clicking any of them, pressing N (focuses se**n**d to),
then V (selects **v**ideo-compare).

To get video-compare to appear in the `Send To` field you will need to open the `send to` folder, which
you can access by typing `shell:sendto` in Run (Windows + R), then simply make a shortcut to `video-compare.exe`.

Thanks to [couleurm](https://github.com/couleurm) for the sharing this tip and creating the screen recording above.

#Batch encoder for VOD websites

##Usage


    ./envoder [optional arguments]

###Optional Arguments:

`--help`

Prints help message and exit


`-i DIR:DIR2:...`
`--input-dirs DIR:DIR2:...`

Input directories to search for video files.

* On Unix, Mac and GNU/Linux: `-i /path/to/dir1:/path/to/dir2:....`
* On Microsoft Mindows: `-i \path\to\dir1;\path\to\dir2\...`

If omited all folders in current working directory (except 'encoded_videos')
will be searched for input video files

`-o DIR, --output-dir DIR`

Output directory to store encoded videos.

* On Unix, Mac and GNU/Linux: `-o /path/to/dir`
* On Microsoft Windows: `-o \path\to\dir`

Default value is ./encoded_videos

`-r, --recursive`

Use this to search sub-directories within the input directories.

Default is not rescurse.

`-w, --overwrite`

Use this if you want to overwrite existing video files.

Default is not overwrite.

`--input-formats FMT1,FMT2,...`

Comma separated list of video formats to process. Other file formats in the
input directories will be ignored.

`--output-format FMT`

Target format for converted videos. Use one of 'mp4', 'mkv', or
other container formats supported by **FFmpeg**.

`--video-encoder ENC`

Video encoder to use. Use one of *h264*, *x264*, *h264*, *mpeg4* variants
for VODs. Use best encoder to use hardware accelerators.

To see supported encoders, run:

    ffmpeg -encoders

`--audio-encoder ENC`

Audio encoder to use. Use one of *mp3*, *aac*, *ogg* variants for VODs.

To see supported encoders, run

    ffmpeg -encoders

`--tolerance TOL`

Tolerance for dimensions.

If one resolution has dimension *width* x *height* and we have
*width1* and *width2* as:

* *width1* = *width* - *TOLERANCE* x *width*
* *width2* = *width* + *TOLERANCE* x *width*

If *width1* <= *video_width* <= *width2*, then video will be assumed
in that resolution.

For example if desired resolution is Full HD (1920x1080) and
*TOLERANCE* is 0.1 then all videos with following condition
will be assumed Full HD:

1920 - 0.1 x 1920 <= *video_width* <= 1920 + 0.1 x 1920

or 1728 <= *video_width* <= 2112

`--dimensions W1xH1,W2xH2,...`

The width and height of the output video, in the format '1280x720'.
On the command line, specify as '-d 1280x720'. You can convert one
file to multiple resolutions with sparating resolutions with comma.

`--faststart`

You can add `-movflags +faststart` as an output option if your videos are
going to be viewed in a browser. This will move some information to the
beginning of your file and allow the video to begin playing before it is
completely downloaded by the viewer. It is not required if you are going
to use a video service such as YouTube. YouTube ​recommends using faststart,
so they can begin re-encoding before uploads complete.

`--upscale`

Use this to upscale videos to higher resolutions.

`--copy-original`

Use this to copy original videos to target directories.

`--ffmpeg-dir DIR`

Directory of the **FFmpeg** executable binary. Set this to the full path
of the directory containing **FFmpeg** executables (*ffmpeg* and *ffprobe*).

On the command line, specify as:

* On Unix, Mac and GNU/Linux: `--ffmpeg-dir /path/to/ffmpeg_dir`
* On Microsoft Windows: `--ffmpeg-dir \path\to\ffmpeg_dir`

`--ffmpeg-suffix SFX`

If you have mutiple version of *FFmpeg*, and *FFmpeg* binaries named like:

* `ffmpeg-4.2.1.exe`, `ffprobe-4.2.1.exe`
* `ffmpeg-3.1.0.exe`, `ffprobe-3.1.0.exe`
* `ffmpeg-dev.exe`, `ffprobe-dev.exe`

you can use them using `--ffmpeg-suffix` command line argument.
For above **FFmpeg** binaries use `-4.2.1`, `-3.1.0` or `-dev`
respectively.


`--logging-level LEVEL`

The minimum severity for an event to be logged on console. Levels
from least severe to most servere are `debug`, `info`, `warning`,
`error`, and `critical`.


`--version`
Prints the version number and exit
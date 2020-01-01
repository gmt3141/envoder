# Batch encoder for VOD websites

## Usage


    ./envoder [optional arguments]

### Optional arguments

---

`--help`

Prints help message and exit

---

`-i DIR:DIR2:...`
`--input-dirs DIR:DIR2:...`

Input directories to search for video files.

* On Unix, Mac and GNU/Linux: `-i /path/to/dir1:/path/to/dir2:....`
* On Microsoft Mindows: `-i \path\to\dir1;\path\to\dir2\...`

If omited all folders in current working directory (except 'encoded_videos')
will be searched for input video files

---

`-o DIR, --output-dir DIR`

Output directory to store encoded videos.

* On Unix, Mac and GNU/Linux: `-o /path/to/dir`
* On Microsoft Windows: `-o \path\to\dir`

Default value is ./encoded_videos

---

`-r, --recursive`

Use this to search sub-directories within the input directories.

Default behaviour is not rescurse into sub-directories.

---

`-w, --overwrite`

Use this if you want to overwrite existing files.

Default behaviour is not overwrite existing files.

---

`--input-formats FMT1,FMT2,...`

Comma separated list of video formats to process. Other file formats in the
input directories will be ignored.

Default input formats are *avi*, *mkv*, *m4v*, *mp4*, *mpg*, *vp9* and *wmv*

---

`--output-format FMT`

Target format for converted videos. Use one of 'mp4', 'mkv', or
other container formats supported by **FFmpeg**.

Default output format is *mp4*

---

`--video-encoder ENC`

Video encoder to use. Use one of *h264*, *x264*, *h264*, *mpeg4* variants
for VODs. Use best encoder to use hardware accelerators.

To see supported encoders, run:

    ffmpeg -encoders

Default video encoder is *libx264*.

---

`--audio-encoder ENC`

Audio encoder to use. Use one of *mp3*, *aac*, *ogg* variants for VODs.

To see supported encoders, run

    ffmpeg -encoders

Default audio encoder is *mp3*.

---

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

Default tolerance is *0.1*.

---

`--dimensions W1xH1,W2xH2,...`

The width and height of the output video, in the format '1280x720'.
On the command line, specify as '-d 1280x720'. You can convert one
file to multiple resolutions with sparating resolutions with comma.

Default dimensions are *7680x4320*, *3840x2160*, *2560x1440*,
*1920x1080*, *1280x720*, *854x480*, *640x360*, *426x240*, *256x144*.

---

`--faststart`

You can add `-movflags +faststart` as an output option if your videos are
going to be viewed in a browser. This will move some information to the
beginning of your file and allow the video to begin playing before it is
completely downloaded by the viewer. It is not required if you are going
to use a video service such as YouTube. YouTube ​recommends using faststart,
so they can begin re-encoding before uploads complete.

Default behaviour is to not add use these option.

---

`--upscale`

Use this to upscale videos to higher resolutions.

Default behaviour is not to upscale to higher resolutions.

---

`--copy-original`

Use this to copy original videos to target directories.

Default behaviour is not copying original videos.

---

`--ffmpeg-dir DIR`

Directory of the **FFmpeg** executable binary. Set this to the full path
of the directory containing **FFmpeg** executables (*ffmpeg* and *ffprobe*).

On the command line, specify as:

* On Unix, Mac and GNU/Linux: `--ffmpeg-dir /path/to/ffmpeg_dir`
* On Microsoft Windows: `--ffmpeg-dir \path\to\ffmpeg_dir`

Default values are:

* On Unix, Mac and GNU/Linux: `/usr/bin`
* On Microsoft Windows: *Current working directory*

---

`--ffmpeg-suffix SFX`

If you have mutiple version of *FFmpeg*, and *FFmpeg* binaries named like:

* `ffmpeg-4.2.1.exe`, `ffprobe-4.2.1.exe`
* `ffmpeg-3.1.0.exe`, `ffprobe-3.1.0.exe`
* `ffmpeg-dev.exe`, `ffprobe-dev.exe`

you can use them using `--ffmpeg-suffix` command line argument.
For above **FFmpeg** binaries use `-4.2.1`, `-3.1.0` or `-dev`
respectively.

Default behaviour is using **FFmpeg** binaries without suffix.

---

`--logging-level LEVEL`

The minimum severity for an event to be logged on console. Levels
from least severe to most servere are *debug*, *info*, *warning*,
*error*, and *critical`*.

Default severity is *info*

---

`--version`

Prints the version number and exit

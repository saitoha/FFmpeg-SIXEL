FFmpeg README
=============

FFmpeg is a collection of libraries and tools to process multimedia content
such as audio, video, subtitles and related metadata.

## Libraries

* `libavcodec` provides implementation of a wider range of codecs.
* `libavformat` implements streaming protocols, container formats and basic I/O access.
* `libavutil` includes hashers, decompressors and miscellaneous utility functions.
* `libavfilter` provides means to alter decoded audio and video through a directed graph of connected filters.
* `libavdevice` provides an abstraction to access capture and playback devices.
* `libswresample` implements audio mixing and resampling routines.
* `libswscale` implements color conversion and scaling routines.

## Tools

* [ffmpeg](https://ffmpeg.org/ffmpeg.html) is a command line toolbox to
  manipulate, convert and stream multimedia content.
* [ffplay](https://ffmpeg.org/ffplay.html) is a minimalistic multimedia player.
* [ffprobe](https://ffmpeg.org/ffprobe.html) is a simple analysis tool to inspect
  multimedia content.
* Additional small tools such as `aviocat`, `ismindex` and `qt-faststart`.

## Documentation

The offline documentation is available in the **doc/** directory.

The online documentation is available in the main [website](https://ffmpeg.org)
and in the [wiki](https://trac.ffmpeg.org).

### Examples

Coding examples are available in the **doc/examples** directory.

## License

FFmpeg codebase is mainly LGPL-licensed with optional components licensed under
GPL. Please refer to the LICENSE file for detailed information.

## Contributing

Patches should be submitted to the ffmpeg-devel mailing list using
`git format-patch` or `git send-email`. Github pull requests should be
avoided because they are not part of our review process and will be ignored.

SIXEL Integration
=============

[![ballmer](https://raw.githubusercontent.com/saitoha/FFmpeg-SIXEL/data/data/ballmer.png)](https://youtu.be/7z6lo4aq6zc)

## Step 0. Edit .Xresources

```
$ cat $HOME/.Xresources
XTerm*decTerminalID: vt340
XTerm*sixelScrolling: true
XTerm*regisScreenSize: 1920x1080
XTerm*numColorRegisters: 256

$ xrdb $HOME/.Xresources  # reload
```

## Step 1. Build xterm with --enable-sixel-graphics option

```
$ wget ftp://invisible-island.net/xterm/xterm.tar.gz
$ tar xvzf xterm.tar.gz
$ cd xterm-*
$ ./configure --enable-sixel-graphics
$ make
$ ./xterm  # launch
```

## Step 2. Build FFmpeg-SIXEL with libsixel

```
$ git clone https://github.com/saitoha/libsixel
$ cd libsixel
$ ./configure && make && make install
$ cd ..
$ git clone https://github.com/saitoha/FFmpeg-SIXEL
$ cd FFmpeg-SIXEL
$ ./configure --enable-libsixel
$ make
$ ./ffmpeg -i a.webm -f sixel -pix_fmt rgb24 -reqcolors 256 -s 600x360 -loglevel panic -
```


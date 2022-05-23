## rawrify-video-compressor

#### A standalone video compressor for Rawrify. I've split this out from the [main Rawrify project](https://github.com/Han-Lon/rawrify) as a subcomponent


### Purpose
I built this to bypass video upload limits on certain social media platforms (e.g. Discord and 8 MB upload limits).

Simply run this program on video(s) you want to upload and it will attempt to compress them, sacrificing video and audio quality to reduce overall size.

There are limitations on how much a video can be compressed, but this works pretty well for most video files I've worked with.

Also includes functionality for converting videos from .mov to .mp4 format, because simply converting to .mp4 reduces size by a significant amount.


### Prerequisites
- Python 3.8+ recommended, but most 3.0+ versions should work
- Install the required Python packages in requirements.txt using `pip install -r requirements.txt`
- Install [ffmpeg](https://ffmpeg.org/) on your local machine
  - Linux - install from relevant package manager
  - Mac - [homebrew recommended](https://formulae.brew.sh/formula/ffmpeg)
  - Windows - [chocolatey recommended](https://community.chocolatey.org/packages/ffmpeg)


### Command line arguments
- `--desired_size` - desired size of the video(s) in Kb; compression target
<br><br>
- `--video_path` - <OPTIONAL> if compressing a video outside of the `input` folder, specify the path here
<br><br>
- `--no-convert-mov` - <OPTIONAL> specify this to NOT convert .mov files to .mp4 before compression. By default, .mov files will be converted.
<br><br>
### How To Use (Multiple Videos and/or Default Video Location)
- Place video files in the `input` directory within this project
- From the command line, execute `python compressor.py --desired_size $SIZE`
  - $SIZE is the desired size of each video file in the `input` folder (what to try to compress to) in Kb
- Wait for the conversion+compression functions to run
- Check the `input` folder for new `*-compressed.mp4` files (the compressed videos)

### How To Use (Individual Video and/or Non-Default Location)
- From the command line, execute `python compressor.py --desired_size $SIZE --video_path $VIDEO_PATH`
  - $SIZE is the desired size of each video file in the `input` folder (what to try to compress to) in Kb
  - $VIDEO_PATH is the path to the video file you want to convert and/or compress
- Wait for the conversion+compression functions to run
- Check the same folder the source video resides in for a new `*-compressed.mp4` file-- this is your compressed video

### Troubleshooting
- If you try to compress a video too much, you will get a "requested bitrate is too low" error from ffmpeg.
  - This can be resolved by increasing the `--desired_size` value. The ffmpeg CLI output will give you an "estimated minimum"-- you can generally go lower than this
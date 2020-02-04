# Convert media with ffmpeg

### Step 1 get information from video
ffprobe -v error -show_entries stream=width,height,bit_rate,duration -of default=noprint_wrappers=1 -sexagesimal {mediaAddress}

### Video convert to sizes
width = 854;height = 480;
ffmpeg -i {mediaAddress} -vf scale={width}:{height} {resultPath}


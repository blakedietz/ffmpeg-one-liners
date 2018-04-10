# ffmpeg-one-liners

## Convert

### Convert mov to mp4

```bash
ffmpeg -i in.mov -vcodec h264 -acodec aac -strict -2 out.mp4
```

## Downsize all files in a directory

```bash
# Look through all files in the current directory
for file in ./*;
do
  ffmpeg -i "$file" -filter:v scale=960:-1 -c:a copy "$file.mp4";
done
```
## Strip out spaces from file names

```bash
for f in *\ *; do mv "$f" "${f// /-}"; done
```

## Concat all videos in a directory into a single video

```bash
# Create a file to load into the concat command
find ./ -type f -print0 | xargs -0 ls -t | while read file
do
    echo file $file >> file-list.txt
done;

# Concatenate all files liste ind the file-list.txt to a single video
 ffmpeg -f concat -safe 0 -i file-list.txt -c copy output.mp4;
```


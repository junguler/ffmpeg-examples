# ffmpeg examples
this repo is dedicated to show examples of how i use ffmpeg for what i do, it plans to cover a wide range of topics in the long run but we'll start with basic every day uses

## what you need to get started
youtube-dl to download royalty free videos from youtube as a source

ffmpeg to demux. mux, convert and apply different filters

primitive, geometrize and gmic for applying different filters to our image sequences

a terminal with access to bash or zsh, if you are on windows this does not come by default but it's very easy to install and use, there are many projects dedicated to bringing bash and other posix tool to linux. among them i recommend: cygwin, git bash for windows, msys2 or wsl/2 if you are a little more advanced

## 1rd step, download a video
```
youtube-dl -f 22 https://www.youtube.com/watch?v=q8Ci8tNAXCI
```
youtube-dl automatically downloads the best quality available but we decided to use the ```-f 22``` switch which tells ```youtube-dl``` we want the 720p mp4 version of the video. you can see all the available quialities of a video by using the ```-F``` switch

once downloaded, we rename the video to ```animals.mp4``` to make our life easier in the next steps

## 2rd step, cut up the video
now that we have the video downloaded it needs to but trimmed sinced it's too long for our purposses, take a look at it in your video player and decide on a a few seconds to make image suquence out of. i've decided to cut the section where the zebras are for example which starts at 47 seconds and ends at 55 seconds
```
ffmpeg -i animals.mp4 -ss 47 -to 55 -c copy zebra.mp4
```
i have intentially decided to start the clip a little sooner and end it a little after because with image sequence we have access to the images themselves and don't need to be exact when trimming.

now for explanation of these switches on ffmpeg do: ```-i``` imports the video, ```-ss``` specifies the starting point of trimming,  ```-to``` the end point of trimming,  ```-c copy``` copies the video and audio quality without conversion.

## 3rd step, make and image sequence out of our clip
```
ffmpeg -y -i zebra.mp4 -c:v mjpeg -q:v 2 -pix_fmt yuvj444p -sn -an -threads 0 image-%06d.jpg
```
now for explanation of these switches on ffmpeg do: ```-c:v mjpeg``` set to use the internal jpg folder of ffmepg, ```-pix_fmt yuvj444p``` specify color mode of our images,  ```-threads 0``` use all available threads of our cpu for speeding up the process, ```image-%06d.jpg``` add image- prefix to all of images and start from the 000000 number and count up, if your clip is shorter you can use smaller digits, we do care that much tho as we are going to mux these after applying filters anyway.

now that you have the image sequence, remove the extra frames from the begining and the end of our sequence

<img src="https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_3_01.jpg" width=45% height=45%>  <img src="https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_3_02.jpg" width=45% height=45%>

## 4rd step, the fun part!
now let's make something beautiful or ugly, your choice, i'll start with an example of using primitive
```
for i in *.jpg; do echo $i; primitive -i $i -o p-$i -n "500" -m "0"; done
```
this converts your image sequnce using the combo option (all available shapes) and adds 500 shapes to every image.
![step4_primitive](https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_4_primitive.jpg)

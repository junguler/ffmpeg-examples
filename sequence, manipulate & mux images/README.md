here i show examples of how to download videos, cut them up to managable clips, make an image sequence out of them, apply various filters to them and mux them back again to get a cool looking gif or video.

## what you need to get started
[youtube-dl](https://youtube-dl.org/) to download royalty free videos from youtube as a source

[ffmpeg](https://www.ffmpeg.org/) to demux. mux, convert and apply different filters

[primitive](https://github.com/fogleman/primitive), [geometrize](https://github.com/Tw1ddle/geometrize-lib-example) and [gmic](https://gmic.eu/) for applying different filters to our image sequences

a terminal with access to bash or zsh, if you are on windows this does not come by default but it's very easy to install and use, there are many projects dedicated to bringing bash and other posix tool to windows. among them i recommend: [cygwin](https://www.cygwin.com/), [git for windows](https://gitforwindows.org/), [msys2](https://www.msys2.org/) or wsl/2 if you are a little more advanced

## first step, download a video
```
youtube-dl -f 22 https://www.youtube.com/watch?v=q8Ci8tNAXCI
```
youtube-dl automatically downloads the best quality available but we decided to use the ```-f 22``` switch which tells ```youtube-dl``` we want the 720p mp4 version of the video. you can see all the available quialities of a video by using the ```-F``` switch

once downloaded, we rename the video to ```animals.mp4``` to make our life easier in the next steps

## second step, cut up the video
now that we have the video downloaded it needs to but trimmed sinced it's too long for our purposses, take a look at it in your video player and decide on a a few seconds to make image suquence out of. i've decided to cut the section where the zebras are for example which starts at 47 seconds and ends at 55 seconds
```
ffmpeg -i animals.mp4 -ss 47 -to 55 -c copy zebra.mp4
```
i have intentially decided to start the clip a little sooner and end it a little after because with image sequence we have access to the images themselves and don't need to be exact when trimming.

now for explanation of these switches on ffmpeg do: ```-i``` imports the video, ```-ss``` specifies the starting point of trimming,  ```-to``` the end point of trimming,  ```-c copy``` copies the video and audio quality without conversion.

## third step, make an image sequence out of our clip
```
ffmpeg -y -i zebra.mp4 -c:v mjpeg -q:v 2 -pix_fmt yuvj444p -sn -an -threads 0 image-%06d.jpg
```
now for explanation of these switches on ffmpeg do: ```-c:v mjpeg``` set to use the internal jpg folder of ffmepg, ```-pix_fmt yuvj444p``` specify color mode of our images,  ```-threads 0``` use all available threads of our cpu for speeding up the process, ```image-%06d.jpg``` add image- prefix to all of images and start from the 000000 number and count up, if your clip is shorter you can use smaller digits, we do care that much tho as we are going to mux these after applying filters anyway.

now that you have the image sequence, remove the extra frames from the begining and the end of our sequence

<img src="https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_3_01.jpg" width=45% height=45%>  <img src="https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_3_02.jpg" width=45% height=45%>

## forth step, the fun part!
now let's make something beautiful or ugly, your choice, i'll start with an example of using primitive
```
for i in *.jpg; do echo $i; primitive -i $i -o p-$i -n "500" -m "0"; done
```
this converts your image sequnce using the combo option (all available shapes) and adds 500 shapes to every image.

![step4_primitive](https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_4_primitive.jpg)

here is another example using gmic-gui to find a good filter and then using that same filter in the terminal for our image sequence:

![gmig-gui](https://github.com/junguler/ffmpeg-examples/blob/main/examples/gmic.jpg)

once you found a good filter you like, click on the button on the top right of the gmic window (highlighted red in above picture) to copy the command and paste it in this loop:
```
for i in *.jpg; do echo $i; gmic $i fx_color_abstraction 1,10,0.2,0,50,50 -o g-$i ; done
```
![step4_gmic](https://github.com/junguler/ffmpeg-examples/blob/main/examples/step_4_gmic.jpg)

more options can be found on the projects web pages [primitive](https://github.com/fogleman/primitive), [geometrize](https://github.com/Tw1ddle/geometrize-lib-example) and [gmic](https://gmic.eu/). i also made some easy bash scripts and batch files for primtiive and geometrize to make your life easier, find them [here for primitive](https://github.com/junguler/easy-primitive-batch) and [here for geometrize](https://github.com/junguler/easy-geometrize-batch)

## final step, muxing the image sequence back together and make a video or gif file
move your converted images to another folder so this loop does not mux them with the originals and lets make a gif out of them:
```
cat *.jpg | ffmpeg -framerate 30 -f image2pipe -i - zebra2.gif
```
or a lossless mp4 video:
```
cat *.jpg | ffmpeg -framerate 30 -f image2pipe -i - -codec copy zebra2.mp4
```
https://user-images.githubusercontent.com/59083599/132505918-dc677c43-858f-473e-b7d6-c81962d79204.mp4

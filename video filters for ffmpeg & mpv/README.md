here i try to show some example of cool looking filters ffmepg has and how easy it is to use them on mpv as a toggle,
make sure ffmpeg is on your $PATH and open the terminal and cd into the clip folder and lets go

### our source clip, i'll try to use the same clip for all the filter examples as to make it easier to compare
https://user-images.githubusercontent.com/59083599/132606268-3f6a1048-e780-4c7c-a100-3a2a45dafe66.mp4

### color manipulation
apply an always changing hue saturation to your video
```
ffmpeg -i based.mp4 -vf "hue=H=0.5*PI*t" rainbow.mp4
```
https://user-images.githubusercontent.com/59083599/132606949-b58d62ab-e249-4e36-b729-6f274c1f1712.mp4

if you to change the speed change ```0.5``` to ```1``` which makes it twice as fast or ```0.25``` to make as half as slow

apply vhs color effect where colors are slightly misplaced on the video
```
ffmpeg -i based.mp4 -vf "rgbashift=rh=-4:bv=+4" fake_vhs.mp4
```
https://user-images.githubusercontent.com/59083599/132607454-fa81c3b4-57f3-42e7-bad2-721f8d8c2171.mp4

just like before, change the values to get a higher or lower effects


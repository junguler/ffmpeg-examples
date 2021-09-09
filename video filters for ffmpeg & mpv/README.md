here i try to show some example of cool looking filters ffmepg has and how easy it is to use them on mpv as a toggle,
make sure ffmpeg is on your $PATH and open the terminal and cd into the clip folder and lets go

## our source clip, i'll try to use the same clip for all the filter examples as to make it easier to compare
https://user-images.githubusercontent.com/59083599/132606268-3f6a1048-e780-4c7c-a100-3a2a45dafe66.mp4

## color manipulation
### apply an always changing hue saturation to your video
```
ffmpeg -i based.mp4 -vf "hue=H=0.5*PI*t" rainbow.mp4
```
https://user-images.githubusercontent.com/59083599/132606949-b58d62ab-e249-4e36-b729-6f274c1f1712.mp4

if you to change the speed change ```0.5``` to ```1``` which makes it twice as fast or ```0.25``` to make as half as slow

### apply vhs color effect where colors are slightly misplaced on the video
```
ffmpeg -i based.mp4 -vf "rgbashift=rh=-4:bv=+4" fake_vhs.mp4
```
https://user-images.githubusercontent.com/59083599/132607659-1a6858bb-23c7-41ad-9014-e41a0cb6b742.mp4

just like before, change the values to get a higher or lower effects

### change the location of the colors slightly without moving the image itself
```
ffmpeg -i based.mp4 -vf "chromashift=cbh=10:cbv=10:crh=-10:crv=-10" chromashift.mp4
```

https://user-images.githubusercontent.com/59083599/132608899-9c675cf2-c6e6-4937-9c28-115a7c639588.mp4

### keep a specific color present and make every other color black & white
```
ffmpeg -i based.mp4 -vf "colorhold=color=00FF00:similarity=0.4:blend=0.1" colorhold.mp4
```
https://user-images.githubusercontent.com/59083599/132608391-a2102a4b-3663-4032-924a-440efa4acf45.mp4

we opted to keep the ```00FF00``` but we could have used ```green``` instead with the same effect, the lesser you set the ```similarity``` the restricter this process becomes, ```blend``` tries to make this effect blend to the other parts of the video and not be too jagged.

## effects, glitches, extras
### apply dithering effect
```
ffmpeg -i based.mp4 -vf "format=monow" dither.mp4
```
https://user-images.githubusercontent.com/59083599/132609761-0db179ad-7210-43b9-ab87-bd27c65adc44.mp4

this filter does not accept extra arguments, because of how the video is converted the true effect is only shown at 50% , 100% , 200% zoom and so on.

### apply posterize effect
```
ffmpeg -i based.mp4 -vf "lutyuv=y=bitand'(val,128+64+32)'" posterize.mp4
```
https://user-images.githubusercontent.com/59083599/132610325-011478a1-b5a7-4cb8-bc1c-702450fe6746.mp4

notice the usage of quotes ```'``` and double quotes ```"``` , sometimes we need to use both in tandom to let ffmpeg know what to do

### apply edge detect effect
this filter has two main uses, one only shows the outline of objects and makes everything else black the other one does that same thing but keeping colors
```
ffmpeg -i based.mp4 -vf "edgedetect" edgedetect.mp4
```
https://user-images.githubusercontent.com/59083599/132611782-e64eab4c-0140-4df3-95ef-b1151b672e81.mp4
```
ffmpeg -i based.mp4 -vf "edgedetect=mode=colormix:high=0" edgecolored.mp4
```
https://user-images.githubusercontent.com/59083599/132611924-aa47dc8c-aeb3-48ba-b79c-60c1239eb77e.mp4

### apply blur to plains but keep edges
```
ffmpeg -i based.mp4 -vf "yaepblur=r=6:s=256" yaepblur.mp4
```
https://user-images.githubusercontent.com/59083599/132612328-4f861d29-b1bb-4a93-a6c1-cb7c2a5a8ecd.mp4

### lagfun! a sort of ghost effect
```
ffmpeg -i based.mp4 -vf "lagfun=decay=0.99" lagfun.mp4
```
https://user-images.githubusercontent.com/59083599/132612713-3255610a-8d9b-4804-a6f7-a294568e2245.mp4


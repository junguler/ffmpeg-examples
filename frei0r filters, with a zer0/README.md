### frei0r filters examples
[frei0r](https://frei0r.dyne.org/) is a free collection of cool looking video filters that does not come built into ffmpeg or mpv by default, 
you need find a version that is specifically compiled for this or compile ffmpeg/mpv yourself and add this library to them
which is outsite of my knowledge and scoop of this repo.

### our source clip, i'll try to use the same clip for all the filter examples as to make it easier to compare
https://user-images.githubusercontent.com/59083599/132966578-cb14f0de-1e9a-4aff-bdbb-b9fcc10d7ab9.mp4

### colortap effect
```
ffmpeg -i based2.mp4 -vf "frei0r=colortap" colortap.mp4
```
https://user-images.githubusercontent.com/59083599/132966644-0a0a0568-2318-49c0-8774-5ec1bf215804.mp4

you can apply this filter as many time as you want just chain them together `-vf "frei0r=colortap,frei0r=colortap"`

### emboss effect
```
ffmpeg -i based2.mp4 -vf "frei0r=emboss" emboss.mp4
```
https://user-images.githubusercontent.com/59083599/132966678-aea90c51-ab88-4de3-9273-427f54c633d7.mp4

### cartoon effect
```
ffmpeg -i based2.mp4 -vf "frei0r=cartoon:0.9999" cartoon.mp4
```
https://user-images.githubusercontent.com/59083599/132966714-5cedd2fa-625d-4ef1-a249-c37dbd977595.mp4

unlike built-in `ffmpeg` filters `0.99` is not 1 percent less than `1` and if you want to amplify a filter effect we have to make it a smaller percentage like `0.75`but in this case we wanted to make the stroke effect less visible so we went with `0.9999` which is way less than `0.99` in how `frei0r` calculates it


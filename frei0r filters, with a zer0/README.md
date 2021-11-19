### frei0r filters examples
[frei0r](https://frei0r.dyne.org/) is a free collection of cool looking video filters that does not come built into ffmpeg or mpv by default, 
you need find a version that is specifically compiled for this or compile ffmpeg/mpv yourself and add this library to them
which is outsite of my knowledge and scoop of this repo.

### quick links
 * [colortap](https://github.com/junguler/ffmpeg-examples/tree/main/frei0r%20filters%2C%20with%20a%20zer0#colortap)
 * [emboss](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#emboss)
 * [cartoon](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0cartoon)
 * [sobel](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#sobel)
 * [vertigo](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#vertigo)
 * [distorter](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#distorter)
 * [light-graffiti](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#light-graffiti)
 * [cluster](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#cluster)
 * [baltan](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#baltan)
 * [ndvi](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#ndvi)
 * [glitchor](https://github.com/junguler/ffmpeg-examples/blob/main/frei0r%20filters,%20with%20a%20zer0#glitchor)

### our source clip, i'll try to use the same clip for all the filter examples as to make it easier to compare
https://user-images.githubusercontent.com/59083599/132966578-cb14f0de-1e9a-4aff-bdbb-b9fcc10d7ab9.mp4

### colortap
```
ffmpeg -i based2.mp4 -vf "frei0r=colortap" colortap.mp4
```
https://user-images.githubusercontent.com/59083599/132966644-0a0a0568-2318-49c0-8774-5ec1bf215804.mp4

you can apply this filter as many time as you want just chain them together `-vf "frei0r=colortap,frei0r=colortap"`

### emboss
```
ffmpeg -i based2.mp4 -vf "frei0r=emboss" emboss.mp4
```
https://user-images.githubusercontent.com/59083599/132966678-aea90c51-ab88-4de3-9273-427f54c633d7.mp4

### cartoon
```
ffmpeg -i based2.mp4 -vf "frei0r=cartoon:0.9999" cartoon.mp4
```
https://user-images.githubusercontent.com/59083599/132966714-5cedd2fa-625d-4ef1-a249-c37dbd977595.mp4

with some `frei0r` filters like this one `0.99` is not 1 percent less than `1` and if you want to amplify a filter effect we have to make it a smaller percentage like `0.75`but in this case we wanted to make the stroke effect less visible so we went with `0.9999` which is way less than `0.99` in how `frei0r` calculates it

### sobel
```
ffmpeg -i based2.mp4 -vf "frei0r=sobel" sobel.mp4
```
https://user-images.githubusercontent.com/59083599/132966919-137912c7-fcde-4c06-b311-2437e95a162d.mp4

### vertigo
```
ffmpeg -i based2.mp4 -vf "frei0r=vertigo" vertigo.mp4
```
https://user-images.githubusercontent.com/59083599/132967043-cd07a872-e58c-403b-a1ac-0763934f7242.mp4

### distorter
```
ffmpeg -i based2.mp4 -vf "frei0r=distort0r:0.02" distorter.mp4
```
https://user-images.githubusercontent.com/59083599/132967092-c681023f-7e39-4177-a6f3-eb7b7aca5bcb.mp4

if you want less distorting change `0.02` to `0.01` for half the movement

### light graffiti
```
ffmpeg -i based2.mp4 -vf "frei0r=lightgraffiti" lightgraffiti.mp4
```
https://user-images.githubusercontent.com/59083599/132967124-95c1203c-cb44-4a30-b661-eaca4d74e6ea.mp4

### cluster
```
ffmpeg -i based2.mp4 -vf "frei0r=cluster" cluster.mp4
```
https://user-images.githubusercontent.com/59083599/132967152-e8cea562-04ce-4094-bf41-f14c42131cb0.mp4

### baltan
```
ffmpeg -i based2.mp4 -vf "frei0r=baltan" baltan.mp4
```
https://user-images.githubusercontent.com/59083599/132967241-accdc944-47de-4932-9585-435fba76e2e8.mp4

### ndvi
```
ffmpeg -i based2.mp4 -vf "frei0r=ndvi" ndvi.mp4
```
https://user-images.githubusercontent.com/59083599/132967270-5f3118cd-69de-463f-a30b-1f8da33fc6c1.mp4

### glitchor
```
ffmpeg -i based2.mp4 -vf "frei0r=glitch0r:0.2" glitchor.mp4
```
https://user-images.githubusercontent.com/59083599/132967301-fd4f3491-9bad-4f7b-9c53-54c10bc71994.mp4

if you want to make glitches twice as more frequent change `:0.2` to `:0.4` likewise if you want to make it happen half as much do `:0.1` or 1 forth the effect `:0.05`

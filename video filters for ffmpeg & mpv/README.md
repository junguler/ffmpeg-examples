here i try to show some examples of cool looking filters ffmepg has and how easy it is to use them on mpv as a toggle,
make sure ffmpeg is on your $PATH and open the terminal and cd into the clip folder and lets go

- [mpv specifics](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#now-for-the-fun-part-using-filters-at-runtime-on-mpv-without-needing-to-convert)

### ffmpeg quick links
 * [ever changing hue saturation](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#color-manipulation)
 * [fake vhs colors](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#apply-vhs-color-effect-where-colors-are-slightly-misplaced-on-the-video)
 * [shift colors](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#change-the-location-of-the-colors-slightly-without-moving-the-image-itself)
 * [keep a color and make other black & white](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#keep-a-specific-color-present-and-make-every-other-color-black--white)
 * [dither effect](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#apply-dithering-effect)
 * [posterize](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#apply-posterize-effect)
 * [edge detect](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#apply-edge-detect-effect)
 * [blur plains and keep edges](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#apply-blur-to-plains-but-keep-edges)
 * [lagfun ghosting effect](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#lagfun-a-sort-of-ghost-effect)
 * [bilateral blur](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#bilateral-a-sort-of-smart-motion-blur)
 * [shuffle frames](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#shuffling-frames-effect)
 * [amplify glitch](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#amplify-a-sort-of-glitch-effect)
 * [tblend glitches](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#tblend-more-glitchiness)
 * [movement emboss effect](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#emboss-effect)
 * [tmix ghosting effect](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#ghost-effect)
 * [kirsch glitch effect](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#kirsch-glitch-effect)
 * [chaining filters](https://github.com/junguler/ffmpeg-examples/tree/main/video%20filters%20for%20ffmpeg%20%26%20mpv#how-about-chaining-filters-together)

## our source clip, i'll try to use the same clip for all the filter examples as to make it easier to compare
https://user-images.githubusercontent.com/59083599/132606268-3f6a1048-e780-4c7c-a100-3a2a45dafe66.mp4

## color manipulation

### apply an always changing hue saturation to your video
```
ffmpeg -i based.mp4 -vf "hue=H=0.5*PI*t" rainbow.mp4
```
https://user-images.githubusercontent.com/59083599/132606949-b58d62ab-e249-4e36-b729-6f274c1f1712.mp4

if you to change the speed change `0.5` to `1` which makes it twice as fast or `0.25` to make as half as slow

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

we opted to keep the `00FF00` but we could have used `green` instead with the same effect, the lesser you set the `similarity` the restricter this process becomes, `blend` tries to make this effect blend to the other parts of the video and not be too jagged.

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

notice the usage of quotes `'` and double quotes `"` , sometimes we need to use both in tandom to let ffmpeg know what to do

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

### bilateral, a sort of smart motion blur
```
ffmpeg -i based.mp4 -vf "bilateral=sigmaS=512,format=yuv420p" bilateral.mp4
```
https://user-images.githubusercontent.com/59083599/132612988-3619ddb9-e45c-4b72-a23d-a50b2ef1c7be.mp4

### shuffling frames effect
```
ffmpeg -i based.mp4 -vf "shuffleframes='9 8 7 6 5 4 3 2 1 0'" shuffle.mp4
```
https://user-images.githubusercontent.com/59083599/132613599-f4f01332-f40f-4765-a227-beb73616f47f.mp4

### amplify, a sort of glitch effect
```
ffmpeg -i based.mp4 -vf "amplify=factor=10:low=5:high=15" amplify.mp4
```
https://user-images.githubusercontent.com/59083599/132613923-48e435df-8ed6-4687-9acc-cd48102bf4f1.mp4

### tblend, more glitchiness 
```
ffmpeg -i based.mp4 -vf "tblend=all_mode=and" tblend_and.mp4
```
https://user-images.githubusercontent.com/59083599/132614621-b9b0605c-b23c-4f1a-aa01-142da87bef92.mp4
```
ffmpeg -i based.mp4 -vf "tblend=all_mode=or" tblend_or.mp4
```
https://user-images.githubusercontent.com/59083599/132614695-706daddf-c5a8-48e3-a94c-d5bda395e516.mp4

### emboss effect
```
ffmpeg -i based.mp4 -vf "tblend=all_mode=grainextract" tblend_emboss.mp4
```
https://user-images.githubusercontent.com/59083599/132614919-245d7afd-6526-4c50-8822-595e2ae66bba.mp4

### ghost effect
```
ffmpeg -i based.mp4 -vf "tmix=frames=16:weights='1'" tmix_ghost.mp4
```
https://user-images.githubusercontent.com/59083599/132615205-9d134396-f77c-4bd5-b9ae-a0c1b0337d5f.mp4

### Kirsch glitch effect
```
ffmpeg -i based.mp4 -vf "kirsch=1" kirsch+.mp4
```
https://user-images.githubusercontent.com/59083599/133453283-f1157a34-94b4-41ce-aebc-7759034aac82.mp4

### how about chaining filters together
chaining filters is easy just use `,` between, feel free to use as many quotes `'` as you need and put everything in double quotes `"` at the end

```
ffmpeg -i based.mp4 -vf "rgbashift=rh=-2:bv=+2,hue=H=0.1*PI*t" tmix_ghost.mp4
```

## now for the fun part, using filters at runtime on mpv without needing to convert

since mpv is compiled with `libavfilter` which is the ffmpeg's library for most of it's filters using them is very easy on mpv, on your terminal do this:
```
mpv --vf="hue=H=0.5*PI*t" based.mp4
```
it's nice but a little cumbersome to open the terminal each time we want to apply some filters, for this reason we'll add these filters and toggles to our `input.conf` , this file does not come with mpv and needs to be made by you. if you are on windows make it in the folder `mpv.exe` is and if you are *nix systems it should be made on `~/.config/mpv/input.conf` now let's put this filter toggle in there and assign a keybind to it.
```
ALT+R vf toggle hue=H=0.5*PI*t 
```
now every time you hit `ALT + R` this video filter `vf` get's toggled, once for on and another time for off and etc ...

chaining multiple filters together is also easy just use `,` between them
```
ALT+B vf toggle hue=H=0.5*PI*t,rgbashift=rh=-2:bv=+2
```
mpv have been recently soft deprecated this way of chaining filters on their git version, it works for the time being but we don't need to worry about when it might gets remove because we can chain these by applying two seperate filters on the same keybind using `;`
```
ALT+B vf toggle hue=H=0.5*PI*t ; vf toggle rgbashift=rh=-2:bv=+2
```
you can also print some informtaion about the filters being applied on mpv's osc (on screen controls), using `show-text` command
```
ALT+R vf toggle hue=H=0.5*PI*t ; show-text "Rainbow Effect"
```
some filters can be applied multiple times to increase their effects, in these cases we use add instead of toggle
```
ALT+N vf add rgbashift=rh=-3:bv=+3
```
every time you press `ALT + N` this filter is going to apply and make the effect more potent, be careful and don't overdo it because we are applying everything on the fly so to speak and there is some little impact on cpu usage with every filter you add

## how do remove these filters when watching videos on mpv?
it's very easy to remove all filters that are currently applied to your video
```
KP0 vf set "" ; show-text "NO Filters"
```
i intentially binded this key to the number zero on the numpad keys as it's gets used often and binding it to two key strokes might get annoying, this keybind can be used as many times as you want and those filters also can be toggled again after clearing filters


## nice, is there a script to test out ffmpeg filters on mpv without adding them to my input.conf
yes, there is an excellent script that does exactly that, download it from here [live-filters](https://github.com/hdb/mpv-live-filters) and put it in your `scripts` folder, if a script didn't work just click the raw button and copy all of the text and paste in into a blank text file and rename it to the name of the script


## i'm a heavy mouse user, what about us?
mpv does not come with a right click menu by default but [uosc](https://github.com/darsain/uosc) is an excellent script that mitigates that and adds a bunch of other cool stuff to the ui too, put it in your scripts folder eithr at `C:\users\USERNAME\AppData\Roaming\mpv\scripts\uosc.lua` on windows or `~/.config/mpv/scripts/uosc.lua` now for making a keybind in the right click menu add this to your `input.conf`
```
mbtn_right  script-binding uosc/menu
#           vf toggle hue=H=0.1*PI*t ; show-text "Frame 2" #! Rainbow Filter
esc         quit #! Quit 
```
this is a very bare example of a menu, it can have multiple nested menus inside it, for more examples either look at the [uosc](https://github.com/darsain/uosc#adding-items-to-menu) page or look at my own [input.conf](https://github.com/junguler/dotfiles/blob/main/mpv/input.conf) which has many examples of how to use this right click menu

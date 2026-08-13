# Using BeatSaberPlus mod, with other mods, on versions below 1.42.0, some UI symbols don't turn into ?s

## So short recap!
Beat Saber on linux doesn't have `Segue UI Symbol` fonts that BSML (Beat Saber Markup Language) uses, so to fix the symbols you need to manually install `seguisym.ttf`

That's all fun, until you use the BeatSaberPlus mod, beacuse that uses `segoeui.ttf` fonts for it's own UI, heck it even installs both `segoeui.ttf` and `seguisym.ttf` on game launch if they're missing.

The problem is that those fonts have overlapping unicode declarations, so.. BSML doesn't really know how to handle that **(This behavior was changed, I was only able to replicate it on version 1.40.8 and below, but this are still recommended version, as of when I'm writing this)**

## The fix
It's rather simple actualy.. you need to merge those fonts!

So get the `segoeui.ttf` and `seguisym.ttf` fonts from a legit copy of windows... or from [this repo](https://github.com/mrbvrz/segoe-ui-linux)

And using something like `fonttools` from pip (`pip install fonttools`), merge them with this command:
`pyftmerge segoeui.ttf seguisym.ttf --output-file=segoeui.ttf`

..or if you don't feel like doing all that, get the merged font from [here](https://github.com/duskoboo/linux-beat-saber-tweaks/blob/main/beat-saber-plus-before-1-42-0/segoeui.ttf)

Either way, make sure the combined font is named `segoeui.ttf`, as that's what BeatSaberPlus uses.

Now take said font, and go to the Fonts directory in the `compatdata`

Path to `compatdata`:
 - Steam: `<your SteamLibary path>/steamapps/compatdata/620980`
 - BSManager: `<your BSManager Installation folder>/SharedContent/compatdata`
 - encore: `~/.config/encore/compatdata`
**(This of course depends on your installation method)**

Path to Fonts directory:
`compatdata/pfx/drive_c/windows/Fonts`

Delete any old `segoeui.ttf` and `seguisym.ttf` fonts, and replace them with your merged font.

And that's it! Enjoy!


# Create new profile and scene
![[Pasted image 20250330175640.png]]
![[Pasted image 20250330175929.png]]
# Setting up camera
Add camera under sources `Video capture device (V4L2)` and name it.

![[Pasted image 20250330175329.png]]
i had to choose `Motion-JPEG`  to get full resolution from my camera.
# Settings
## Video Settings
Press `Settings` in the lower right corner and go to `Video`.
Here you need to set the canvas and output to be the resolution of your camera (i put a bit smaller horizontal to get 16:9 resolution)
![[Pasted image 20250330184314.png]]
## Audio settings
Press `Settings` in the lower right corner and go to `Output -> Recording`
There you will see a dropdown for type, choose `Custom Ouput (FFmpeg)`
![[Pasted image 20250330180422.png]]
Choose `matroska` as container format, and we can set the video bitrate up for better quality (depending on camera, i have logitech Brio 4K so i can bump significantly)

Video encoder as default

Further down on same page, put the audio bitrate to `320 Kbps` for best sound quality, check the Audio Track `1`, and use the `pcm_s24le` setting for the Audio encoder
![[Pasted image 20250330180619.png]]

Now change to the Audio tab, still in the `Output` settings and change the tracks audio bitrate to `320`
![[Pasted image 20250330180740.png]]

Now go to the main audio settings under `Audio` on the left hand side.
Set the sample rate to `48 kHz` and channels to `Mono`.
Here you can also set up your microphone as a global audio device. I have set my audio interface as the  `Mic/Auxiliary Audio`
![[Pasted image 20250330180840.png]]

# Setting up voice activation border

## Mask filter
Create or download an image mask like this:
![[square_image_mask.png]]

Add a Color source
![[Pasted image 20250330190906.png]]
 Set the color to the desired border color:
 ![[Pasted image 20250330190953.png]]
Size it to the whole canvas.

Exit that menu and choose the color source in the sources window and press `Filters` right above that
![[Pasted image 20250330191052.png]]

Add the filter `Image/Mask Blend` and choose type `Alpha Mask (Color Channel)`, input the mask image, set the color to white (`#ffffff`) at 1 `opacity`.

You should now have a border around your cam.
## Set up automatic hide/show

Install the advanced scene switcher plugin https://obsproject.com/forum/resources/advanced-scene-switcher.395/

May have to restart OBS for it to pop up, but it should be in the tools dropdown at the top of the screen ![[Pasted image 20250330190725.png]]

Set up two macros, one for showing the border and one for hiding it.
For the top window add an `if`
set `if` the `Audio` at `Output volume` for your `Audio source` (`Mic/Aux` if you set it the same as me with global), `is above` a threshold you set.

Bottom window, use `Set item visibility` on `Current scene` to show the Color source item in sources. like this (i named mine `Voice Activated Border`):
![[Pasted image 20250330191523.png]]

And then you make another one like it, but this time for `below` the same threshold, and `Hide` instead of show, like this:
![[Pasted image 20250330191747.png]]

As you can see i also set a duration modifier. So that the border is at least shown for half a second. Press the clock icon to do this.

And now you should have a voice activated border in OBS!

# Cam to discord
I cannot use my same camera in discord with this setup (directly), to circumvent this you can use the output from OBS as a virtual camera and use this. Just toggle the `Start Virtual Cam` button in the bottom left corner of the main wnidow. And you should now have a `fake cam` option in discord to use.

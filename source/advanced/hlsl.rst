HLSL Effects for Windows
========================

By default, MAME outputs an idealized version of the video as it would be on the way to the arcade cabinet's monitor, with minimal modification of the output (primarily to stretch the game image back to the aspect ratio the monitor would traditionally have, usually 4:3) -- this works well, but misses some of the nostalgia factor. Arcade monitors were never ideal, even in perfect condition, and the nature of a CRT display distorts that image in ways that change the appearance significantly.

Modern LCD monitors simply do not look the same, and even computer CRT monitors cannot match the look of an arcade monitor without help.

That's where HLSL comes into the picture.

HLSL simulates most of the effects that a CRT arcade monitor has on the video, making the result look a lot more authentic. However, HLSL requires some effort on the user's part: the settings you use are going to be tailored to your PC's system specs, and especially the monitor you're using. Additionally, there were hundreds of thousands of monitors out there in arcades. Each was tuned and maintained differently, meaning there is no one correct appearance to judge by either. Basic guidelines will be provided here to help you, but you may also wish to ask for opinions on popular MAME-centric forums.


Resolution and Aspect Ratio
---------------------------

Resolution is a very important subject for HLSL settings. You will want MAME to be using the native resolution of your monitor to avoid additional distortion and lag created by your monitor upscaling the display image.

While most arcade machines used a 4:3 ratio display (or 3:4 for vertically oriented monitors like Pac-Man), it's difficult to find a consumer display that is 4:3 at this point. The good news is that that extra space on the sides isn't wasted. Many arcade cabinets used bezel artwork around the main display, and should you have the necessary artwork files, MAME will display that artwork. Turn the artwork view to Cropped for best results.

Some older LCD displays used a native resolution of 1280x1024, which is a 5:4 aspect ratio. There's not enough extra space to display artwork, and you'll end up with some very slight pillarboxing, but the results will be on-par with a 4:3 monitor.


Getting Started with HLSL
-------------------------

You will need to have followed the initial MAME setup instructions elsewhere in this manual before beginning. Official MAME distributions include HLSL by default, so you don't need to download any additional files.

Open your MAME.INI in your text editor of choice (e.g. Notepad), and make sure the following options are set correctly:

* **video d3d**
* **filter 0**

The former is required because HLSL requires Direct3D support. The latter turns off extra filtering that interferes with HLSL output.

Lastly, one more edit will turn HLSL on:

* **hlsl_enable 1**

Save the .INI file and you're ready to begin.


Tweaking HLSL Settings inside MAME
----------------------------------

For multiple, complicated to explain reasons, HLSL settings are no longer saved when you exit MAME. This means that while tweaking settings is a little more work on your part, the results will always come out as expected.

Start by loading MAME with the game of your choice (e.g. **mame pacman**)

The tilde key (**~**) brings up the on-screen display options. Use up and down to go through the various settings, while left and right will allow you to change that setting. Results will be shown in real time as you're changing these settings.

Once you've found settings you like, write the numbers down on a notepad and exit MAME.


Configuration Editing
---------------------

As referenced in :ref:`advanced-multi-CFG`, MAME has a order in which it processes INI files. The HLSL settings can be edited in MAME.INI, but to take full advantage of the power of MAME's config files, you'll want to copy the HLSL settings from MAME.INI to one of the other config files and make changes there.

For instance, once you've found HLSL settings you think are appropriate for Neo Geo games, you can put those settings into neogeo.ini so that all Neo-Geo games will be able to take advantage of those settings without needing to add it to every game INI manually.


Configuration Settings
----------------------

| **hlslpath**
| 
| 	This is where your HLSL files are stored. By default, this will be the HLSL folder in your MAME installation.
| 
| **hlsl_prescale_x**
| **hlsl_prescale_y**
| 
| 	The factor at which the initial pre-HLSL picture will be prescaled before the effects are applied. The higher the prescale, the better the results (within reason) but the more video card power is used. If HLSL is giving you severe slowdown, you can try decreasing these. A value of 0 will cause HLSL to automatically calculate based on display resolution, but you may want to set it higher for better effect if your hardware can handle it.
| 
| **hlsl_snap_width**
| **hlsl_snap_height**
| 
| 	Sets the resolution that Alt+F12 HLSL screenshots are output at.
| 	
| **shadow_mask_alpha**
| 
| 	This defines how strong the effect of the shadowmask is. Acceptable range is from 0 to 1, where 0 will show no shadowmask effect, 1 will be a completely opaque shadowmask, and 0.5 will be 50% transparent.
| 	
| **shadow_mask_texture**
| **shadow_mask_x_count**
| **shadow_mask_y_count**
| **shadow_mask_usize**
| **shadow_mask_vsize**
| 
| 	These settings need to be set in unison with one another. In particular, **shadow_mask_texture** sets rules for how you need to set the other options.
| 	
| 	**shadow_mask_texture** sets the texture of the shadowmask effect. Three shadowmasks are included with MAME: *adapture-grill.png*, *shadow-mask.png*, and *slot-mask.png*
| 	
| **shadow_mask.png settings:**
| 
| 	shadow_mask_texture shadow-mask.png
| 	shadow_mask_x_count 6
| 	shadow_mask_y_count 4
| 	shadow_mask_usize 0.1875
| 	shadow_mask_vsize 0.25
| 
| 	The use of shadow_mask.png requires special care. While shadow_mask_x_count and shadow_mask_y_count can be increased, the shadow_mask_x_count to shadow_mask_y_count ratio must remain 3:2 to avoid graphical glitching.
| 
| 	The settings shadow_mask_uoffset and shadow_mask_voffset can be used to tweak the alignment of the final shadowmask, as the results can differ on different combinations of video card and monitor.
| 
| **slot-mask.png settings:**
| 
| 	shadow_mask_texture slot-mask.png
| 	shadow_mask_x_count 6
| 	shadow_mask_y_count 6
| 	shadow_mask_usize 0.1875
| 	shadow_mask_vsize 0.1875
|
| 	You can increase the shadow_mask_x_count and shadow_mask_y_count, but keep the shadow_mask_x_count and shadow_mask_y_count identical to one another to avoid graphical glitching.
| 
| 	The settings shadow_mask_uoffset and shadow_mask_voffset can be used to tweak the alignment of the final shadowmask, as the results can differ on different combinations of video card and monitor.
| 
| **adapture-grill settings:**
| 
| 	shadow_mask_texture adapture-grill.png
| 	shadow_mask_x_count 6
| 	shadow_mask_y_count 6
| 	shadow_mask_usize 0.1875
| 	shadow_mask_vsize 0.1875
| 	
| 	You can increase the shadow_mask_x_count and shadow_mask_y_count, but keep the shadow_mask_x_count and shadow_mask_y_count identical to one another to avoid graphical glitching.
| 
| 	The settings shadow_mask_uoffset and shadow_mask_voffset can be used to tweak the alignment of the final shadowmask, as the results can differ on different combinations of video card and monitor.
| 
| 
| **curvature**
| 
| 


Random Notes
------------
Delete this section when you finish this chapter.

[23:56] <@Tafoid> Firehawke:  Windows can use GLSL shaders when using -video opengl
[23:57] <@Tafoid> but none are distributed by default, I believe
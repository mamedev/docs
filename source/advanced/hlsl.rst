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
| **curvature**
| 
| 	This setting determines how strong of a fisheye effect the curvature should be.
|
| **round_corner**
| 
| 	The corners of the display can be rounded off through the use of this setting.
| 
| **smooth_border**
| 
| 	Sets a smoothened/blurred border around the edges of the screen.
| 
| **reflection**
| 
| 	If set above 0, this creates a white reflective blotch on the display. By default, this is put in the upper right corner of the display. By editing the POST.FX file's GetSpotAddend section, you can change the location. [todo: What's the max?]
| 
| **vignetting**
| 
| 	When set above 0, will increasingly darken the outer edges of the display in a pseudo-3D effect. [todo: What's the max?]
| 
| **scanline_alpha**
| 
| 	This defines how strong the effect of the scanlines are. Acceptable range is from 0 to 1, where 0 will show no scanline effect, 1 will be a completely black line, and 0.5 will be 50% transparent. Note that arcade monitors did not have completely black scanlines.
| 
| **scanline_size**
| 
| 	The overall spacing of the scanlines is set with this option. Setting it at 1 represents consistent alternating spacing between display lines and scanlines.
| 
| **scanline_height**
| 
| 	This determines the overall size of each scanline. Setting lower than 1 makes them thinner, larger than 1 makes them thicker.
| 
| **scanline_bright_scale**
| 
| 	Specifies how bright the scanlines are. Larger than 1 will make them brighter, lower will make them dimmer. Setting to 0 will make scanlines disappear entirely.
| 
| **scanline_bright_effect**
| 
| 	This will give scanlines a glow/overdrive effect, softening and smoothing the top and bottom of each scanline.
| 
| **scanline_jitter**
| 
| 	Specifies the wobble or jitter of the scanlines, causing them to jitter on the monitor. Warning: Higher settings may hurt your eyes.
| 
| **defocus**
| 
| 	This option will defocus the display, blurring individual pixels like an extremely badly maintained monitor. Specify as X,Y values (e.g. **defocus 1,1**)
| 
| **converge_x**
| **coverge_y**
| 
| 	Adjust the convergence of the red, green, and blue channels in a given direction. Many badly maintained monitors with bad convergence would bleed colored ghosting off-center of a sprite, and this simulates that.
| 
| **red_ratio**
| **grn_ratio**
| **blu_ratio**
| 
| 	Defines a 3x3 matrix that is multiplied with the RGB signals to simulate color channel interference. For instance, a green channel of (0.100, 1.000, 0.250) is weakened 10% by the red channel and strengthened 25% through the blue channel.
| 
| **offset**
| 
| 	Strengthen or weakens the current color value of a given channel. For instance, a red signal of 0.5 with an offset of 0.2 will be raised to 0.7
| 
| **scale**
| 
| 	Applies scaling to the current color value of the channel. For instance, a red signal of 0.5 with a scale of 1.1 will result in a red signal of 0.55
| 
| **power** (*RGB Gamma*)
| 
| 	Exponentiate the current color value of the channel. This is called RGB-Gamma in the slider menu. For instance, a red signal of 0.5 with red power of 2 will result in a red signal of 0.25
| 	
| 	This setting also can be used to adjust line thickness in vector games.
| 
| **floor**
| 
| 	Sets the absolute minimum color value of a channel. For instance, a red signal of 0.0 (total absense of red) with a red floor of 0.2 will result in a red signal of 0.2
|
| 	Typically used in conjunction with artwork turned on to make the screen have a dim raster glow.
| 
| **phosphor_life**
| 
| 	How long the color channel stays on the screen (phosphor ghosting)-- 0 gives absolutely no ghost effect, and 1 will leave a contrail behind that is only overwritten by a higher color value.
| 
| 	This also affects vector games quite a bit.
| 
| **saturation**
| 
| 	Color saturation can be adjusted here.
| 
| **bloom_scale**
| 
| 	Determines the intensity of bloom effect. Arcade CRT displays had a tendency towards bloom, where bright colors could bleed out into neighboring pixels. This effect is extremely graphics card intensive, and can be turned completely off to save GPU power by setting it to 0
| 
| **bloom_overdrive**
| 
| 	Sets a RGB color, separated by commas, that has reached the brightest possible color and will be overdriven to white. This is only useful on color raster games.
| 
| **bloom_lvl0_weight**
| **bloom_lvl1_weight**
|      .  .  .  .
| **bloom_lvl9_weight**
| **bloom_lvl10_weight**
| 
| 	These define the bloom effect. If used carefully in conjuction with phosphor_life, glowing/ghosting for moving objects can be achieved.
|
| Suggested defaults for raster-based games:
| 

+-------------------------------+------------------+-------------------------------------------+
| | bloom_lvl0_weight     1.00  | | Bloom level 0  | | (full-size target) weight. (0.00-1.00)  |
| | bloom_lvl1_weight     0.64  | | Bloom level 1  | | (half-size target) weight.(0.00-1.00)   |
| | bloom_lvl2_weight     0.32  | | Bloom level 2  | | (1/4-size target) weight. (0.00-1.00)   |
| | bloom_lvl3_weight     0.16  | | Bloom level 3  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl4_weight     0.08  | | Bloom level 4  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl5_weight     0.04  | | Bloom level 5  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl6_weight     0.04  | | Bloom level 6  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl7_weight     0.02  | | Bloom level 7  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl8_weight     0.02  | | Bloom level 8  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl9_weight     0.01  | | Bloom level 9  | | (.) weight.  (0.00-1.00)                |
| | bloom_lvl10_weight    0.01  | | Bloom level 10 | | (1x1 target) weight.  (0.00-1.00)       |
+-------------------------------+------------------+-------------------------------------------+

Random Notes
------------
Delete this section when you finish this chapter.

[23:56] <@Tafoid> Firehawke:  Windows can use GLSL shaders when using -video opengl
[23:57] <@Tafoid> but none are distributed by default, I believe
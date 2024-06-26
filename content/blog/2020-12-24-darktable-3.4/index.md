---
title: "darktable 3.4: Encore!"
author: the darktable team
slug: darktable-3-4
date: 2020-12-24
lede: deer.jpg
lede_author: Chris Elston
tags:
  - announcement
  - darktable-release
aliases:
    - /2020/12/darktable-3-4/  
---
Translations of this article: [German](https://www.bilddateien.de/blog/2020-12-24-darktable-3-4-weiteres-update.html), [French](https://darktable.fr/2020/12/darktable-3-4-la-revolution-colorimetrique-continue/)

Happy holidays everyone -- it's time for your favourite Christmast gift. This is the second major release of 2020 from the darktable project following the early release of darktable 3.2 in August, and we've been busy: between the darktable, rawspeed, and dtdocs repos, there have been more than 5,500 commits in 2020!

# Documentation

Photography is a difficult enough endevor and trying to manage your post-processing without documentation can make things even harder!  This time, though, the darktable team has been busy getting the user manual ready in time for the release and it is available today at https://www.darktable.org/resources/, and fully up-to-date with the latest version.

## New Markdown Documentation!

You know how it is though... You wait ages for an up-to-date user manual and then two come along at once! The current version of the user manual has served us well for the last 10 years, but has now reached the end of its life. It used a complicated XML software stack in order to compile it into HTML or PDF and this complexity steers away many contributors as well as being hard to build locally.

So for darktable version 3.4 we are also releasing the first version of the new user manual, now split into a separate project named "dtdocs". We have completely reorganised and rewritten the manual into a more maintainable structure using Markdown. This project has involved new content as well as a significant overhaul of the text, making it much easier to read for native English speakers.

For now, this project not ready to entirely take over from the existing documentation, so it will co-exist (in English only) with the old version, which is being retained for the in-application help links and translations. The dtdocs project will take over completely with translations as part of darktable 3.6.

The darktable 3.4 version of dtdocs can be found at https://www.darktable.org/usermanual/en/ and it is maintained at https://github.com/darktable-org/dtdocs/.

A similar project is also underway to transfer lua documentation to Markdown. This project is expected to be ready in the coming months and is currently maintained at https://github.com/darktable-org/luadocs/.

# Performance Enhancements

Who doesn't like to go faster, right?

Many of the computationally-intensive image processing algorithms have been updated to be faster and more scaleable when running on the CPU. Improved operations include nonlocal means denoising (used by denoise (non-local means) and denoised (profiled)), bilateral filter (used by local contrast, color mapping, global tonemapping, lowpass, monochrome, retouch, and shadows & highlights), and the guided filter (used by haze removal and drawn mask feathering).

Much unnecessary recomputation has been eliminated, leading to a more responsive user interface while editing an image in the darkroom. The display of parametric and channel masks shows a particularly marked improvement.

In addition, filmic RGB version 4 now works with OpenCL and highlight reconstruction is now significantly faster with OpenCL-enabled hardware.

# New Module: Color Calibration

The color revolution in darktable continues! This time, the _channel mixer_ module has been swallowed up by a new module, _color calibration_.

![the color calibration module](color-calibration-module.png)

There are a number of issues within the existing channel mixer module that cannot be resolved without adversely impacting older edits. At the same time as resolving all of these issues, the new module also offers improved white balancing, or _Chromatic Adaptation_.

White balancing is only a part of chromatic adaptation, which more globally aims at simulating how the current scene would appear if it had been lit by another illuminant (in this case, by the display illuminant). While white balance only cares about ensuring highlights end up neutral, chromatic adaptation is concerned with the full color range. The new module uses channel mixing with precomputed parameters, which usually produces more vibrant and pleasing colors, especially for skin tones.

Since chromatic adaptation is actually a channel mixer in disguise, it has been decided to turn the new channel mixer into a full-featured hub for color corrections. This module allows users to fine-tune the camera input profiles (another channel mixer in disguise), perform robust illuminant adaptation with Bradford transform (used by ICC v4) and CAT16 (from the CIE CAM 2016), apply creative cross-talk color grading. It also allows users to sanitize the pipeline input gamut with non-destructive gamut compression and (as a last resort) destructive gamut clipping, to help when dealing with the infamous blue LED lights. The gamut compression aims at keeping luminance unchanged and hue as close as possible to the original, while reducing saturation until the whole image fits into the gamut of the working color space.

This new module can be used in conjuction with masks, which enables selective illuminant correction for cases where several colored light sources are present, and no global adaptation can fix them all. It provides a full library of CIE standard illuminants as well as two machine-learning algorithms which can find the most likely illuminant for the scene when no neutral color can be sampled in the image. It can also use the white balance written in the EXIF metadata of the raw file and will use this as a default setting.

A few B&W film presets are provided in the module to emulate color to monochrome conversions. Unlike the presets in the old channel mixer, which had no real physical basis, these are computed from the spectral sensitivity of film emulsions and properly white-balanced in spectral domain, so they are closer to actual film response (aside from the local silver reactions).

A new "modern" processing workflow, disabled by default, allows you to use the _color calibration_ to perform white-balancing in place of the _white balance_ module for new edits. You can enable it manually in the preferences (processing tab).

Other than that, _color calibration_ will allow you to darken or brighten the image in a color-preserving way, using pixel values (in the same spirit as _filmic_) for example to quickly darken skies. Finally, it can affect saturation in a channel-dependent way, again using _filmic_ v4 color science (which is **not** hue linear).

Full documentation of the new module is available [here](https://www.darktable.org/usermanual/en/module-reference/processing-modules/color-calibration/).

See also the announcement notification and discussion at [discuss.pixls.us](https://discuss.pixls.us/t/introducing-color-calibration-module-formerly-known-as-channel-mixer-rgb/21227/40) or the [YouTube video](https://youtu.be/U4CEN0JPcoM).

# Filmic RGB Visualisation Modes

Three new visualisation modes have been added to the filmic RGB module to aid user understanding of its functionality.

Of particular note is the _dynamic range mapping_ view. This view is inspired by the Ansel Adams Zone System, showing in 1-dimensional how the EV zones in the input scene are mapped to the output. Middle grey from the scene is, by default, mapped to 18% in the output (linear) space. This visualisation shows how the tonal ranges towards the extremes of the scene exposure range are compressed into a smaller number of zones in the display space, leaving more room for the mid-tones to be spread out over the remaining zones. This view has been designed to replace the usual tone curve view, which hides under a 2-dimensional graph the very important fact that what is tone is a 1-dimensional intensity shuffle from input range to output range.

![the dynamic range mapping view](filmic-rgb-dyanmic-range-mapping.png)

Please see the [user manual](https://www.darktable.org/usermanual/en/module-reference/processing-modules/filmic-rgb/) for more information.

# Tone Equalizer Improvements

One of the main issues with the current version of the Tone Equalizer module is that the guided filter algorithm tends to smooth the highlights much less than it smooths the shadows, and to be more sensitive to vertical/horizontal edges than to diagonal ones. The latest release of darktable introduces a new default exposure-independent guided filter (eigf) specially developed by the darktable team, that resolves some of these issues while also significantly improving the module's performance.

![tone equalizer module's masking tab](tone-equlizer-masking.png)

The available smoothing algorithms for the 'preserve details' control are now as follows:

 - no
 - guided filter
 - average guided filter
 - eigf _(default)_
 - averaged eigf

You can find detailed descriptions of the smoothing algorithms in the [documentation](https://www.darktable.org/usermanual/en/module-reference/processing-modules/tone-equalizer/).

# Linear Scene Referred Blending

Currently, most blending modes clip pixel values at 100%, which makes them unsuited for scene-referred adjustments. Recall that a display-referred pipeline forces pixel values between 0 and 100%, relative to the display white luminance. This is a limitation for HDR imagery because it needs to be non-linearly force-fit into that range early in the pipe, losing color along the way. Scene-referred workflows keep pixel intensities unbounded for as long as possible and defer the non-linear range mapping to the last step in the pipe, allowing for correct alpha compositing and optical filters within the pipe, no matter the dynamic range of the scene.

![the new blend modes](blend-modes.png)

Also, RGB parametric masking uses an HSL color model, in which pixels greater than 100% will produce negative saturation. So, even with unbounded blending modes, it still does not work with scene-referred.

As a result, a new blending and masking mode has been introduced. This mode uses only unbounded blending operators, and introduces a _boost_ factor that allows you to mask pixels up to 18 EV above 100% display. For robust and consistent masking, it introduces the JzCzhz color space, which is a luma/chroma/hue perceptual color space with the same logic as Lch (from CIE Lab 1976), but designed for HDR and showing near-perfect hue linearity. It is computed from the JzAzBz space published in 2017.

While JzCzhz is a non-linear space, it is used only to produce an opacity/transparency mask from the image, and the actual blending is done in the native colorspace of the module. Also, the JzCzhz space is computed using the current color profile of the module, which means that the same parametric masking will produce the same hue mask before or after the input color profile.

This enhancement also comes with a slight speed-up of the masking and blending code.

Along with these new blending capabilities, the parametric mask UI has been tidied up to hide the output mask sliders by default. These can be re-enabled from the blend mode menu. See [the manual](https://www.darktable.org/usermanual/en/darkroom/masking-and-blending/overview/) for more details.

# Module Groups

![managing the module groups](module-groups.png)

Many users have requested customization of module groups, and now that feature is here! Processing modules in the darkroom can now be assigned to user-defined module groups. This replaces the previous "favourites" group and the "more modules" module with a tool that allows you to create your own module groups and presets based on your workflow. A number of default presets are included.  See [the manual](https://www.darktable.org/usermanual/en/darkroom/interacting-with-modules/search-and-group/) for details.

# Clipping Warning

Currently, the darkroom's over-exposure preview highlights pixels where any of the 3 RGB channels lie outside of a range defined by upper and lower thresholds. This information is not very helpful since that kind of clipping can come from a mix of luminance clipping (true overexposure) and gamut clipping (oversaturation or lack of proper gamut-mapping). Users take this indicator very seriously and frequently get confused by the information displayed.

darktable 3.4 replaces the over-exposure preview with a new "clipping warning" which combines the luminance and gamut clipping indicators into a single utility. Please see [the manual](https://www.darktable.org/usermanual/en/module-reference/utility-modules/darkroom/clipping/) for full documentation of this new mode. Note that the gamut warning is still available for now but is largely superseded by the new functionality.

![the new clipping indicator](clipping-indicator.png)

# Export Print Sizes

The lighttable export module now provides the ability to calculate the size of the final exported image in pixels by entering either

- A scale factor, to be applied to the size of the original image (after cropping); or
- The height and/or width of the exported image in inches or centimetres, along with the desired DPI

![export file size in inches](export-file-size.png)

# Map View Changes

Great news for geotagging enthusiasts! Images that are close together are now grouped within the map view and a count of the grouped images displayed. This improves performance in situations where many images in a collection have location data stored. Mouse-scrolling over an image group cycles through the grouped images. Groups containing selected images are highlighted with a white border. The image count is displayed as a white number if all images of the group are exactly at the same place, and in yellow otherwise.

![the new map view](map-view.png)

A new [_locations_](https://www.darktable.org/usermanual/en/module-reference/utility-modules/map/locations/) module has been added, allowing you to create areas or locations and organize them using hierarchical tags.

# Preferences

The following enhanements have been made to the preferences & settings dialog:

- Altered preferences (those that have been changed from their default values) are now indicated with a bullet symbol
- If preferences are changed that require a restart in order to take effect, a message will appear to remind you to restart when exiting the preferences dialog
- A number of preferences have been altered such that they no longer require a restart to take effect
- The 'CSS theme tweaks' functionality in the General tab now has a more intuitive workflow -- press the "save and apply" button to apply your CSS immediately without having to first select the "modify theme with CSS tweaks" checkbox. This checkbox can still be used to temporarily disable your modifications in case of error.

# Presets

- New option to hide built-in presets
- New option to display built-in or user presets first

# Deprecated Modules

The following processing modules are deprecated in darktable 3.4. These modules will continue to be available for old edits and can still be accessed for new edits via the "modules: deprecated" module group preset. However be warned that from version 3.6, these modules will no longer be available for new edits.

- The _channel mixer_ module is superseded by the _color calibration_ module.
- The _invert_ module is superseded by the _negadoctor_ module.
- The _fill light_ and _zone system_ modules are now superseded by the _tone equalizer_ module.
- The _global tonemap_ and _tone mapping_ modules are superseded by the _filmic rgb_ and _local contrast_ modules

# Renamed Modules

The following modules have been renamed to better describe their use. These modules can still be found using their old names in the module search box.

- _denoise (non-local means)_ is now _astrophoto denoise_
- _denoise (bilateral filter)_ is now _surface blur_


# UI Enhancements

Many existing modules have had updates to their UI

- The _retouch_ and _white balance_ module layouts have been completely rewritten
- It is now possible to choose different UI layouts for the _color balance_ module, in order to reduce its height
- The _tone curve_ and _base curve_ modules have been aligned to use a common interface
- A number of utility modules can now have their height adjusted by hovering your mouse over them and pressing _Ctrl+scroll_.
- The darkroom _history stack_ module now shows the changes that have been made between history items when you hover the mouse over the module
- The _global color picker_ module UI has been overhauled
- It is now possible to automatically hide the header buttons on processing modules in the darkroom
- Hovering your mouse over the header of a processing module now displays a  tooltip providing detailed in-app documentation.

# Other Changes

- The tethering view has been reworked to improve stability and now includes the histogram module again
- A new button has been added to enable focus peaking mode, to complement the existing keyboard shortcut
- Clicking on the darkroom history stack module's reset button provides a one-click way to discard history on your current image
- The history stack can now be truncated -- removing all history items above the selected one but without compressing -- in the darkroom by holding _Ctrl_ while clicking the "compress history stack" button
- New functionality has been added to `darktable-cli`
- The filter categories combobox in the _collect images_ are now organized into groups
- The data and library databases are now regularly checked for corruption
- Backups of the data and library databases are now taken automatically allowing you to easily restore to an earlier state in case of corruption
- By default the copy button now exclude some modules that can cause issues when pasted between images. You can still include these modules by using the "copy parts" button
- Automatic module presets can be reapplied by holding _Ctrl_ while clicking on the module's reset button
- Importing of images from a camera in Windows should be more stable, as the gPhoto API is no longer used
- Side panels can be made narrower with fewer graphical glitches, allowing you to reserve more screen real-estate for your images
- Read support for 16-bit (half) float TIFFs has been added
- Greyscale support has been added for the AVIF format
- A new preset has been added to the denoise (profiled) module to remove only chrominance noise using wavelets mode

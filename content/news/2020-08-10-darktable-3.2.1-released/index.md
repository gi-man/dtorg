---
author: Pascal Obry
date: 2020-08-10 20:20:23+00:00
layout: post
title: darktable 3.2.1 released
lede: araignee.jpg
lede_author: <a href="http://photos.obry.net">Pascal Obry</a>
tags:
  - announcement
  - darktable release
aliases:
    - /2020/08/darktable-321-released/
---
We're proud to announce the new feature release of darktable, 3.2.1!

Note that 3.2.0 has been skipped due to last minute bug fixes.

The github release is here: [https://github.com/darktable-org/darktable/releases/tag/release-3.2.1](https://github.com/darktable-org/darktable/releases/tag/release-3.2.1).

As always, please don't use the autogenerated tarball provided by
github, but only our tar.xz. the checksums are:

```
$ sha256sum darktable-3.2.1.tar.xz
6e3683ea88dc0a0271be7eca4fd594b9e46b1b7194847825a8d0a0c12bdeb90c darktable-3.2.1.tar.xz
$ sha256sum darktable-3.2.1.dmg
292b8327fdc2bd6346994d52f904e0d89078100c91eec2a7c6982f71f8dd24ca darktable-3.2.1.dmg
$ sha256sum darktable-3.2.1.exe
7d21442aa31a627428cf9e56c85ecb4e985b544ea950d98b54ed0a6f123ad6d3 darktable-3.2.1.exe
```

When updating from the current stable 3.0.x series, please bear in
mind that your edits will be preserved during the upgrade, but the new
library and configuration files are not backward compatible; they're not usable with 3.0.x, so
making a backup is strongly advised.

#### Important note: to make sure that darktable can keep supporting the raw file format from your camera, *please* read [this post](https://discuss.pixls.us/t/raw-samples-wanted/5420?u=lebedevri) on how/what raw samples you can contribute to ensure that we have the *full* raw sample set for your camera under CC0 license!

- Almost 2700 commits to darktable+rawspeed since 3.0
- 790 pull requests handled
- 92 issues closed
- Updated user manual is coming soon™

## The Big Ones

- The *lighttable* view has been rewritten and the filmstrip reworked, resulting in large performance gains, especially when using the zoomable lighttable view. The culling view has also been rewritten from scratch. Operations are smooth at any screen resolution up to 8k.

  Many types of overlay are now possible on lighttable thumbs. Different overlay
  information can be selected depending on the thumb size on the
  lighttable. The different sizes can be set in the preferences, so we
  can have no overlay at all for small thumbs and full overlay when
  large thumbs are displayed. This is fully configurable.

  Likewise, the tooltip information when hovering the thumbs can be
  activated/deactivated based on the thumbs size.

- The lighttable modules have improved user interaction: buttons are highlighted
  only when the context makes the action
  possible.

- A complete overhaul of the CSS has been done. This gives
  darktable a professional look. This continues
  the goal to make every single aspect of the UI themable using CSS.

- The Color Picker and
  Location modules are updated to better fit into the new UI, and most of the icons
  have been altered so as to be more visually balanced.

- The preference dialog has been fully reviewed and reorganized to
  propose a better look and require less
  scrolling. It is also possible to add some CSS rules directly into
  the preference dialog to tweak darktable's look as well as
  to directly control the font size and DPI values from the general
  preference tab.

  A search field has been added to the shortcuts tab to help you find
  the keyboard shortcut you want to customize.

- The new negadoctor module has been added to help inverting negative
  films.

- A new histogram display called RGB Parade has been added. At the
  same time the histogram module height can now be adjusted with
  <kbd>Ctrl+Scroll</kbd>.

- The metadata feature has been made generic internally and has new
  features. The user can now select the information they want to see in the
  metadata editor. This selection is automatically mirrored in the collection
  and image information modules.

  Along with a new "notes" field, all the fields are multiline
  <kbd>Ctrl+Enter</kbd>, sizable <kbd>Ctrl+Scroll</kbd> and can be set
  as private (not exported). Metadata collection filters have an entry
  "not defined". At import time it is possible to choose not to import
  some metadata.

- Image change detection has been made more reliable. This affects the
  lighttable thumbnails change symbol and history collection filter,
  which is now more accurate. In darkroom navigation, this avoids the
  need to recalculate an image and save the xmp file when there is no change.

- A new down-sampling preference has been introduced for faster
  response in darkroom. The preview is either computed at full
  resolution (original, default value) or at 1/2, 1/3 or 1/4 of the
  original size. This allow for better performance but can slightly
  hinder the precision of the guided filter masking.

  Note that this is a very delicate feature to implement. A lot of care has
  been taken to ensure all is correct when using down sampling. It
  touches all areas of darktable, like masks, guided filter, liquify
  controls, crop & rotate, lens and perspective corrections...

- Clarify the three possible workflows. Previous version had a preference
  to choose whether to auto-apply the base curve module. Many questions were
  raised about the intention. The new preference introduces three workflows:

  display-referred : use base-curve module

  scene-referred   : use filmic and exposure modules (new default)

  none             : use neither base-curve nor filmic

- Filmic RGB is updated to v4 (new color science) with integrated highlight recovery.

## New Features And Changes

- Add support for curved gradients. This can be helpful when putting a gradient mask on an image with a horizon line that is curved due to lens distortion. This can also be for artistic goals.

- Add support for AVIF file format (requires [libavif](https://github.com/AOMediaCodec/libavif) >= 0.7)

- Collect module has two new filters: module and module order.

  The former makes it possible to filter pictures based on the
  activated modules in the history. The latter can be used to filter
  based on the pipe version (legacy up to 2.6 releases or v3.0
  starting with 3.0 release).

- Tag in the Collect module keeps track of the selected images order.

  When a tag is at the first level of the Collect module, any change
  on the images order is kept along with the selected tag.
  This allows to the user to associate a specific order with every image (tag)
  collection.

- A full rewrite of the pipe ordering has been done. It is now
  possible to change the order of the pipe using a new module giving
  access to the legacy order (order used up to 2.6 releases) and the
  v3.0 order. It is also
  possible to create module order presets which can be freely applied.

  Note that the copy/paste of multi-instances when they have been
  reordered in a way that some other modules are separating them will
  not keep the same order. This was buggy in previous implementation
  when the target image had also been reordered in a non-compatible
  manner or using a different pipe order. In this new versions all the
  multi-instances will be grouped together keeping their relative
  order.

  Note that this work has mainly been done to make the implementation
  simpler, safer and that will require less maintenance. Also as this
  implementation records the full pipe order for history and styles it
  will be the ground for proposing different strategies when applying
  styles.

- The retouch module has a new keyboard shortcut "show or hide shapes" which can
  be mapped to a key to quickly show or hide shapes. This is in
  addition to the right-click on the image which does the same action.

- The spot removal module keyboard shortcut to show-hide shapes has been renamed
  to "show or hide shapes" for clarity and to be consistent with
  the new keyboard shortcut in the retouch module.

- It is possible to change the color of all overlays (shapes, guides,
  etc), in the darkroom. This may come handy on some images where the gray
  guides were barely visible. The possible colors are now: Grey,
  Red, Green, Yellow, Cyan, Magenta. The colors can be cycled through
  using <kbd>Ctrl+O</kbd>.

- In the crop & rotate module, the pan movements can be restricted
  vertically or horizontally using the <kbd>Shift</kbd> or
  <kbd>Control</kbd> respectively.

- The crop & rotate module now allows format ratios to be entered as
  a float number.

- When using a snapshot view, a flag has been added to clearly show the
  position of the snapshot.

- Improve the falloff and radius of the vignette to 200% for better
  control.

- Add a user-defined mode in the white-balance module to keep the last
  modification of the module. It is then possible to go back to the
  last modified setting after selecting another mode (spot for
  example).

- Dynamic keyboard shortcuts have been added for combo-boxes making it
  possible to select next and previous values directly from the
  keyboard.

- It is now possible to adjust the color picker areas just after
  having created them. This is achieved by dragging one of the four
  little square handles at the corner.

- Tagging improvements: Entry tag(s) creation works now without an image
  selected.  It allows the user to create a tag on a virtual node, to insert
  a pipe <kbd>|</kbd> character in create tag (menu). The tree display
  shows the newly created tags.

- New variables $(LENS), $(EXIF_EXPOSURE_BIAS), $(VERSION_NAME) and
  $(VERSION_IF_MULTI) have been defined. $(CATEGORYn(category)) works
  now when multiple values on the same image (for example people) and
  accepts 9 levels instead of 3 (for n).

- Four new timestamps are now supported to store the import, last
  export, last change and last print times. Those timestamps are also
  made available in the collection module and so can be used to better
  control of created collections.

- Multiple image drag & drop works now on map view.

- Add new preferences for keyboard shortcuts to control how
  multi-instances are handled (use first or last instance, prefer the
  visible, active or expanded instance). This also fixes some faults
  caused when duplicating or deleting modules, and when selecting
  earlier edits in the history stack.

- Introspection support has been added into darktable. At this time
  this does not bring new features for end-users but it has provided a
  basis for significant simplification of the code. This will provide easier
  integration of new modules and will ensure better interactivity
  consistency between modules.

- Add optional grey-scale export of TIFF for monochrome images.

- Add some tooltip information for tone equalizer.

- Some actions, like cropping, have been made more responsive by triggering a
  fast-pipe mode where the quality of the image is less important
  while dragging the controls.

- Better support for HiDPI icons theme on Windows.

- Add keyboard shortcut for enabling/disabling tooltips <kbd>Shift+T</kbd>.

- Better history stack module order (more logical) for newly-imported images.

- Add confirmation when deleting/updating presets.

- It is possible to handle (deleting, applying or exporting) multiple
  styles in the style module.

- Applying a style now supports overwrite mode (it previously could
  only append to the existing history stack). This makes the style module
  consistent with the copy/paste of history.

- Rework the sliders to make then look better (smaller and controls a
  bit more visible).

- Implement undo/redo for orientation changes from the lighttable.

- Exported pictures size should be more conservative and stable when
  flip or orientation is changed.

- Using <kbd>Ctrl+Click</kbd> in the blending module drawn masks, it is possible to
  allow continuous creation of masks.

  Continuous mask creation was previously the default in the retouch and spot
  removal modules. For consistency this has been changed and so now one need to use
  <kbd>Ctrl+Click</kbd> in these modules as well for continuous mask creation.

- Rejecting an image still keeps the last number of stars. So
  un-rejecting it will recover the previous star rating.

- Improve messages when a database lock is detected to give better
  guidance about the possible solutions, checks to be done for
  recovering from this situation.

- Rework local laplacian implementation for a 2x speed-up.

- Optimize the denoise profile module (bilateral filter) for better
  performance.

- Many parts of the histogram code have been reworked for better
  performance.

- A new universal toast message framework has been put in place. This
  is used to display information about changes performed with dynamic
  keyboard shortcuts when the module is collapsed.
  It gives visual information about the change being made
  (like exposure change or new opacity value, etc.).

- The spot removal module has been enhanced to be more consistent with
  the functionality of the retouch module. A new button has been added
  to show/hide shapes. It also now supports continuous shape creation.

- Add a new keyboard shortcut to toggle last snapshot on/off.

- Add a new keyboard shortcut to show/hide lib modules.

- Add a new keyboard shortcut to show/hide drawn masks for the currently active module

- Allow for more than 500 images in tethered control which is needed
  for time-lapse.

- It is now possible to export masks in TIFF format.

- Duplicate modules now use the new metadata field "version name" in place
  of the title field to show a description of each image version

- Fix support of legacy parameters in the basic adjustment module.

- Add integrated database maintenance policy.

## Bug fixes

- Better performance when using masks.

- Fix some displayed images issues.

- Fix to allow the shift modifier to be used in dynamic keyboard shortcuts.

- Fix exporting private tags issue with different settings along the path.

- Fix possible freeze on liquify module.

- Fix long text display when no space is available to show all the text by using an ellipsis.
  This allows the side panels to be reduced in size without adversely
  affecting the UI.

- Fix some crop & rotate issues.

- Smoother transition for gradient shapes.

- Fix the snapshot rotation which could go 180° in a single click.

- Add missing icon for the tone-mapping module.

- Fix color-zone module min & max indicator in edit by area mode.

- Enhance performance of blending and retouch, tone equalizer,
  color-picker modules when masks are set on/off and/or removing some
  unnecessary reprocessing.

- Various minor fixes to the shape selection buttons in the retouch module

- Fix displayed curve in denoise profile Y0U0V0 mode.

- Film rolls can be ordered by folder name or id (so in chronological
  order).

- Fix gphoto camera detection procedure.

- Fix the opacity issue (second attempt) which led to a mask having no effect.

- Fix a possible infinite loop in the slideshow module.

- Fix a possible out-of-bound indexing in the chromatic aberration module.

- Fix issues when importing duplicates.

- Fix possible race condition in tone equalizer module.

## Notes

- A known issue when using two computers to edit images. If the three
  following options activated:

  - update database from selected xmp files
  - write sidecar file for each image
  - check xmp on start

  then darktable will write the XMP for each images each time you switch
  from one computer to another. This is due to an issue with the way
  timestamps are implemented and is being fixed for 3.4.

  You can follow the discussion here:
  https://github.com/darktable-org/darktable/pull/5869

  A safe option if you are in this specific case is to wait to 3.4 release
  planned at the end of year.

- The histogram has been deactivated on the print view because after
  lot of work on the histogram code it was not possible to have it
  ready for this view. The work on this part is almost ready now so
  the print view will get back its histogram for the 3.4 release.

- An integration test suite has been added. This will ensure better
  quality and keeping old edits intact. This is an important tool for
  developers to ensure a rework of a module for performance reason
  for example does not change visually the image.

## Lua

- API changed to 6.0.0

- facebook, flickr, and picasa removed from types.dt_imageio_storage_module_t.

- piwigo added to type.dt_imageio_storage_module_t.

- notes and version_name metadata fields added to types.dt_lua_image_t data type.

- Added 4 new properties to dt_collection_properties_t,
  DT_COLLECTION_PROP_IMPORT_TIMESTAMP, DT_COLLECTION_PROP_CHANGE_TIMESTAMP,
  DT_COLLECTION_PROP_EXPORT_TIMESTAMP, DT_COLLECTION_PROP_PRINT_TIMESTAMP

- added darktable.gui.panel_get_size and darktable.gui.panel_set_size functions
  to set the width of the  left or right panels and the height of the bottom panel.

- fixed is_password field of entry widget to work according to the API manual, so
  now when it is set to true the field is hidden.

- Added function darktable.gui.views.lighttable.is_image_visible to check if an image
  is visible in lighttable view.

- Added function darktable.gui.views.lighttable.set_image_visible to force an
  image to be visible in lighttable view.

- Added a lua scripts installer to the default luarc

## Changed Dependencies


## RawSpeed changes

- New Panasonic 'V6' decompressor
- Huffman table implementations rewrite/cleanup
- Fuji compressed raw decompressor performance improvements (-13% wall clock)
- Canon CRW decoding performance improvements (-15% wall clock)
- DNG LJpeg decompressor support for images with 2 components / pixel
- DNG Deflate decompressor support for images with more than 1 component / pixel
- Fuji compressed raw decompressor support for 16-bit raws
- Continuation of ongoing collaboration with LLVM, highlights include many
  little steps towards making it possible to auto-vectorize GoPro's VC5
  decompressor loops, Canon S-RAW interpolator loops; more changes upcoming.


## Camera support, compared to 3.0.0

### Base Support

- Fujifilm FinePix S1
- Fujifilm GFX 100 (compressed)
- Fujifilm X-Pro3 (compressed)
- Fujifilm X-T200
- Fujifilm X-T4 (compressed)
- Fujifilm X100V (compressed)
- Hasselblad H4D-50
- Hasselblad X1D II 50C
- Hasselblad X1DM2-50c
- Nikon COOLPIX P950 (12bit-uncompressed)
- Nikon D780 (12bit-compressed, 14bit-compressed)
- Nikon Z 50 (12bit-compressed, 14bit-compressed)
- Olympus E-M1MarkIII
- Olympus E-PL10
- Panasonic DC-FZ10002 (3:2)
- Panasonic DC-GX880 (4:3)
- Panasonic DC-S1 (3:2)
- Panasonic DC-S1H (3:2)
- Panasonic DC-S1R (3:2)
- Panasonic DC-TZ91 (4:3)
- Panasonic DC-TZ95 (4:3)
- Panasonic DC-TZ96 (4:3)
- Panasonic DC-ZS80 (4:3)
- Panasonic DMC-FZ40 (1:1, 3:2, 16:9)
- Panasonic DMC-FZ45 (1:1, 3:2, 16:9)
- Sony ILCE-6100
- Sony ILCE-9M2

### White Balance Presets

- Canon EOS 77D
- Canon EOS 9000D
- Fujifilm X-E3
- Fujifilm X-T30
- Fujifilm X-T4
- Nikon COOLPIX P1000
- Olympus E-M1MarkIII
- Olympus E-PL6
- Olympus TG-5
- Panasonic DC-GH5
- Panasonic DC-TZ95
- Panasonic DC-TZ96
- Panasonic DC-ZS80
- Samsung NX1
- Sony ILCE-7RM4

### Noise Profiles

- Canon EOS-1Ds
- Fujifilm X-H1
- Fujifilm X-T100
- Fujifilm X-T30
- Fujifilm X-T4
- Nikon COOLPIX P1000
- Nikon Z 50
- Olympus E-510
- Olympus E-M1MarkIII
- Olympus E-M5 Mark III
- Olympus TG-6
- Panasonic DC-GF9
- Panasonic DC-GX800
- Panasonic DC-GX850
- Panasonic DC-GH5
- Panasonic DC-TZ95
- Panasonic DC-TZ96
- Panasonic DC-ZS80
- Sony DSC-RX100M6
- Sony DSC-RX100M7
- Sony ILCE-6600
- Sony ILCE-7RM4
- Sony ILCE-9
- Sony ILCE-9M2


## Translations

- German
- European Spanish
- French
- Hebrew
- Italian
- Polish
- Brazilian Portuguese
- Russian
- Slovenian

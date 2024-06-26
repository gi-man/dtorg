---
author: Pascal Obry
date: 2018-12-03 20:03:00+00:00
layout: post
title: darktable 2.6.0rc0 released
lede: etretat.jpg
lede_author: <a href="http://photos.obry.net">Pascal Obry</a>
tags:
  - announcement
  - darktable release
aliases:
    - /2018/12/darktable-260rc0-released/
---
we're proud to announce the first release candidate for the upcoming 2.6 series of darktable, 2.6.0rc0!

the github release is here: [https://github.com/darktable-org/darktable/releases/tag/release-2.6.0rc0](https://github.com/darktable-org/darktable/releases/tag/release-2.6.0rc0).

as always, please don't use the autogenerated tarball provided by github, but only our tar.xz. the checksums are:

```
$ sha256sum darktable-2.6.0~rc0.tar.xz
5317f6353a1811ffc1e4c06fb983db5cd0bcfdccd6d8f595f470a3536424658f darktable-2.6.0rc0.tar.xz
$ sha256sum darktable-2.6.0rc0.dmg
??? darktable-2.6.0rc0.dmg
$ sha256sum darktable-2.6.0rc0.exe
??? darktable-2.6.0rc0.exe
```

when updating from the currently stable 2.4.x series, please bear in mind that your edits will be preserved during this process, but it will not be possible to downgrade from 2.6 to 2.4.x any more.

#### Important note: to make sure that darktable can keep on supporting the raw file format for your camera, *please* read [this post](https://discuss.pixls.us/t/raw-samples-wanted/5420?u=lebedevri) on how/what raw samples you can contribute to ensure that we have the *full* raw sample set for your camera under CC0 license!

- Over 1600 commits to darktable+rawspeed since 2.4
- 260+ pull requests handled
- 250+ issues closed
- Updated user manual is coming soon™

## The Big Ones

- new module retouch allowing changes based on image frequency layers
- new module filmic which can replace the base curve and shadows and highlights
- new module to handle duplicates in the darkroom with possibility to add a title, create standard or virgin duplicate, delete duplicate and quickly compare with a duplicate
- new logarithm controls for the tone-curve
- new mode for the unbreak profile module
- add mask preview to adjust size, hardness before placing them
- make it possible to change the cropped area in the perspective correction module
- the mask blur has been complemented with a guided-filter to fine tune it (this works on RGB and Lab color space).
- color balance module has two new modes based on ProPhotoRGB and HSL
- Experimental support for PPC64le architecture (OpenCL support needs to be disabled, `-DUSE_OPENCL=OFF`)

## New Features And Changes

- search from the map view is now fixed
- visual rework of the lighttable (color label, image kind, local copy)
- an option make it possible to display some image information directly on the thumb
- add optional scrollbars on lighttable, or lighttable and darkroom
- allow each masks of the clone module to have the opacity adjusted
- lightroom import module supports the creator, rights, title, description and publisher information.
- enhance TurboPrint support by displaying the dialogue with all possible options
- new sort filter based on the image's aspect
- new sort filter based on the image's shutter speed
- new sort filter based on the image's group
- new sort filter based on a personalized sorting order (drag&drop on the lighttable view)
- collection based on the local copy status
- group image number displayed on the collection module
- new zoom level at 50%; 400%, 800% and 1600%
- better support for monochrome RAW
- add contextual help pointing to the darktable's manual
- better copy/paste support for multiple instances
- add support for renaming the module instances
- add frequency based adjustment for the RAW denoise module
- add frequency based adjustment for the denoise profile module
- all widgets should be themable via CSS now
- add support for configuring the modules layout
- different way to select hierarchical tags in the collection module (only the actual parent tag, all children or the parent and children)
- better handling of grouped images by allowing setting stars, color label for the whole group.
- make it possible to apply a preset to a new module instance using the middle click
- new script to migrate collection from Capture One Pro

## Bug fixes

- Fix the color pickers behavior in all modules
- Fix liquify tools switching
- Many more bugs got fixed

## Lua

- No changes

## Changed Dependencies

- CMake 3.4 is now required
- In order to compile darktable you now need at least gcc-5.0+/clang-3.9+
- Minimal clang version was bumped from 3.4+ to 3.9+
- Packagers are advised to pass ```-DRAWSPEED_ENABLE_LTO=ON``` to CMake to enable partial LTO.

## RawSpeed changes

- GoPro '.GPR' raws are now supported via new, fast 'VC-5' parallel decompressor
- Panasonic's new raw compression ('.RW2', GH5s, G9 cameras) is now supported via new fast, parallel 'Panasonic V5' decompressor
- Panasonic's old (also '.RW2') raw decompressor got rewritten, re-parallelized
- Phase One ('.IIQ') decompressor got parallelized
- Nikon NEF 'lossy after split' raw support was recovered
- Phase One ('.IIQ') Quadrant Correction is now supported
- Olympus High-Res (uncompressed) raw support
- Lot's and lot's and lot's of maintenance, sanitization, cleanups, small rewrites/refactoring.
- NOTE: Canon '.CR3' raws are *NOT* supported as of yet.

## Camera support, compared to 2.4.0

### Base Support

- Canon EOS 1500D
- Canon EOS 2000D
- Canon EOS Rebel T7
- Canon EOS 3000D
- Canon EOS 4000D
- Canon EOS Rebel T100
- Canon EOS 5D Mark IV (sRaw1, sRaw2)
- Canon EOS 5DS (sRaw1, sRaw2)
- Canon EOS 5DS R (sRaw1, sRaw2)
- Canon PowerShot G1 X Mark III
- Fujifilm X-A5
- Fujifilm X-H1 (compressed)
- Fujifilm X-T100
- Fujifilm X-T3 (compressed)
- GoPro FUSION (dng)
- GoPro HERO5 Black (dng)
- GoPro HERO6 Black (dng)
- GoPro HERO7 Black (dng)
- Hasselblad CFV-50
- Hasselblad H5D-40
- Hasselblad H5D-50c
- Kodak DCS Pro 14nx
- Kodak DCS520C
- Kodak DCS760C
- Kodak EOS DCS 3
- Nikon COOLPIX P1000 (12bit-uncompressed)
- Nikon D2Xs (12bit-compressed, 12bit-uncompressed)
- Nikon Z 6 (except uncompressed raws)
- Nikon Z 7 (except 14-bit uncompressed raw)
- Olympus E-PL8
- Olympus E-PL9
- Olympus SH-2
- Panasonic DC-FZ80 (4:3)
- Panasonic DC-G9 (4:3)
- Panasonic DC-GH5S (4:3, 3:2, 16:9, 1:1)
- Panasonic DC-GX9 (4:3)
- Panasonic DC-TZ200 (3:2)
- Panasonic DC-TZ202 (3:2)
- Panasonic DMC-FZ2000 (3:2)
- Panasonic DMC-FZ2500 (3:2)
- Panasonic DMC-FZ35 (3:2, 16:9)
- Panasonic DMC-FZ38 (3:2, 16:9)
- Panasonic DMC-GX7MK2 (4:3)
- Panasonic DMC-ZS100 (3:2)
- Paralenz Dive Camera (chdk)
- Pentax 645Z
- Pentax K-1 Mark II
- Pentax KP
- Phase One P65+
- Sjcam SJ6 LEGEND (chdk-b, chdk-c)
- Sony DSC-RX0
- Sony DSC-RX100M5A
- Sony DSC-RX10M4
- Sony DSC-RX1RM2
- Sony ILCE-7M3

### White Balance Presets

- Canon EOS M100
- Leaf Credo 40
- Nikon D3400
- Nikon D5600
- Nikon D7500
- Nikon D850
- Olympus E-M10 Mark III
- Olympus E-M1MarkII
- Panasonic DC-G9
- Panasonic DC-GX9
- Panasonic DMC-FZ300
- Sony DSC-RX0
- Sony ILCE-6500
- Sony ILCE-7M3
- Sony ILCE-7RM3

### Noise Profiles

- Canon EOS 200D
- Canon EOS Kiss X9
- Canon EOS Rebel SL2
- Canon EOS 750D
- Canon EOS Kiss X8i
- Canon EOS Rebel T6i
- Canon EOS 760D
- Canon EOS 8000D
- Canon EOS Rebel T6s
- Canon EOS 77D
- Canon EOS 9000D
- Canon EOS 800D
- Canon EOS Kiss X9i
- Canon EOS Rebel T7i
- Canon EOS M100
- Canon EOS M6
- Canon PowerShot G1 X Mark II
- Canon PowerShot G1 X Mark III
- Canon PowerShot G9 X
- Fujifilm X-T3
- Fujifilm X100F
- Nikon COOLPIX B700
- Nikon D5600
- Nikon D7500
- Nikon D850
- Olympus E-M10 Mark III
- Olympus TG-5
- Panasonic DC-G9
- Panasonic DC-GX9
- Panasonic DMC-FZ35
- Panasonic DMC-FZ38
- Panasonic DMC-GF6
- Panasonic DMC-LX10
- Panasonic DMC-LX15
- Panasonic DMC-LX9
- Panasonic DMC-TZ70
- Panasonic DMC-TZ71
- Panasonic DMC-ZS50
- Pentax K-01
- Pentax KP
- Samsung NX1
- Sony DSC-RX100M4
- Sony DSC-RX10M3
- Sony ILCE-7M3

## Translations

- Afrikaans
- Czech
- German
- Finnish
- French
- Galician
- Hebrew
- Hungarian
- Italian
- Norwegian Bokmål
- Nepal
- Dutch
- Portuguese
- Romanian
- Russian
- Slovenian
- Albanian
- Thai
- Chinese

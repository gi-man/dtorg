---
author: Pascal Obry
date: 2021-02-06 09:50:00+00:00
layout: post
title: darktable 3.4.1 released
lede: archi.jpg
lede_author: <a href="http://photos.obry.net">Pascal Obry</a>
tags:
  - announcement
  - darktable release
aliases:
    - /2021/02/darktable-341-released/
---
We're proud to announce the new feature release of darktable, 3.4.1!

The github release is here: [https://github.com/darktable-org/darktable/releases/tag/release-3.4.1](https://github.com/darktable-org/darktable/releases/tag/release-3.4.1).

As always, please don't use the autogenerated tarball provided by
github, but only our tar.xz. the checksums are:

```
$ sha256sum darktable-3.4.1.tar.xz
7fc3f851da9bcd7c5053ecd09f21aa3eb6103be98a6c58f52010b6f22174941e darktable-3.4.1.tar.xz

$ sha256sum darktable-3.4.1.dmg
e13112ed1d5f9c55e5287aa9d7276f04b90909b2e356640f36227a0a53321658 darktable-3.4.1.dmg

$ sha256sum darktable-3.4.1-win64.exe
94f6f0999378a541b25bd030838b508882d2bace86a95c898a30ca32c406c3f8 darktable-3.4.1-win64.exe
```

When updating from the currently stable 3.2.x series, please bear in
mind that your edits will be preserved during this process, but the new
library and configuration will not be usable with 3.2.x any more, so
you are strongly advised to take a backup first.

#### Important note: to make sure that darktable can keep on supporting the raw file format for your camera, *please* read [this post](https://discuss.pixls.us/t/raw-samples-wanted/5420?u=lebedevri) on how/what raw samples you can contribute to ensure that we have the *full* raw sample set for your camera under CC0 license!

- Almost 100 commits to darktable+rawspeed since 3.4
- 25 pull requests handled
- 18 issues closed

## The Big Ones

None

## New Features And Changes

- Faster thumbnail generation during import.

- Some minor CSS improvements.

## Bug fixes

- Fix color correction RGB handling and saturation normalization.

- Fix smooth scrolling on MacOS.

- Fix Lr metadata import, this is done only if no other XMP present.

- Fix metadata export which must be done only if the corresponding
  setting is activated.

- Fix combo-box popup scrolling.

- Properly restore collection hinter messages when needed.

- Fix stars display in overlay.

- Fix black point setting when dragging the histogram.

- Fix help links for technical group module.

- Properly discriminate cameras with the same prefix in collect module.

- Fix bold rendering on Windows (for selected presets for example).

- Fix support of Windows PATH to configuration and libraries when the
  path name contains non ASCII characters.

- Properly hide the selected tag tick when a tag is not selected anymore.

- Fix search on collect module for multiple filename separated with coma.

- Fix size of clipping handle when preview down-sampling is activated.

- Fix metadata comment reading from exif.

- Fix a case where the thumbnail could be out of synchronization with
  the darkroom edit.

- Never show filmstrip cursor on selected image on other views.

- Skip possible null dates on the collect module which could then
  crash darktable.

- Fix waveform histogram rendering on MacOS.

- Fix some memory leaks.

## Notes


## Lua

## Changed Dependencies


## RawSpeed changes


## Camera support, compared to 3.4.0

### White Balance Presets

- Fujifilm X-Pro3
- Fujifilm X100V
- Olympus E-M10 Mark IV

### Noise Profiles

- Canon EOS 1500D
- Canon EOS 2000D
- Canon EOS Rebel T7
- Canon EOS-1D X Mark II
- Fujifilm X-Pro3
- Fujifilm XF10
- Nikon Z 5
- Panasonic DC-S1R
- Pentax K-1 Mark II
- Sony DSC-RX10M4

## Translations

- Afrikaans
- Czech
- German
- European Spanish
- Finnish
- French
- Hebrew
- Hungarian
- Italian
- Polish
- Brazilian Portuguese
- Russian
- Slovak
- Slovenian

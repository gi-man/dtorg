---
author: jo
comments: true
date: 2015-11-16 18:45:44+00:00
layout: post
link: /2015/11/second-release-candidate-for-darktable-2-0/
slug: second-release-candidate-for-darktable-2-0
title: second release candidate for darktable 2.0
lede: cannobio2.jpg
wordpress_id: 3855
tags:
  - announcement
  - darktable release
---
we're proud to announce the second release candidate in the new feature release of darktable, 2.0~rc2.

as always, please don't use the autogenerated tarball provided by github, but only our tar.xz.

the release notes and relevant downloads can be found attached to this git tag:
[https://github.com/darktable-org/darktable/releases/tag/release-2.0rc2](https://github.com/darktable-org/darktable/releases/tag/release-2.0rc2)
please only use our provided packages ("darktable-2.0.rc2.*" tar.xz and dmg) not the auto-created tarballs from github ("Source code", zip and tar.gz). the latter are just git snapshots and will not work! here are the direct links to tar.xz and dmg:
[https://github.com/darktable-org/darktable/releases/download/release-2.0rc2/darktable-2.0.rc2.tar.xz](https://github.com/darktable-org/darktable/releases/download/release-2.0rc2/darktable-2.0.rc2.tar.xz)
[https://github.com/darktable-org/darktable/releases/download/release-2.0rc2/darktable-2.0.rc2.dmg](https://github.com/darktable-org/darktable/releases/download/release-2.0rc2/darktable-2.0.rc2.dmg)

the checksums are:

    $ sha256sum darktable-2.0~rc2.tar.xz
    9349eaf45f6aa4682a7c7d3bb8721b55ad9d643cc9bd6036cb82c7654ad7d1b1  darktable-2.0~rc2.tar.xz
    $ sha256sum darktable-2.0~rc2.dmg
    f343a3291642be1688b60e6dc98930bdb559fc5022e32544dcbe35a38aed6c6d  darktable-2.0~rc2.dmg

packages for individual platforms and distros will follow shortly.

for your convenience, robert hutton collected build instructions for quite a few distros in our wiki:

[https://redmine.darktable.org/projects/darktable/wiki/Building_darktable_20](https://redmine.darktable.org/projects/darktable/wiki/Building_darktable_20)

the changes from rc1 include many minor bugfixes, such as:

* high iso fix for exif data of some cameras
* various macintosh fixes (fullscreen)
* fixed a deadlock
* updated translations

and the preliminary changelog as compared to the 1.6.x series can be found below.

when updating from the currently stable 1.6.x series, please bear in mind that your edits will be preserved during this process, but it will not be possible to downgrade from 2.0 to 1.6.x any more. be careful if you need darktable for production work!

happy 2.0~rc2 everyone :)

* darktable has been ported to gtk-3.0
* new thumbnail cache replaces mipmap cache (much improved speed, less crashiness)
* added print mode
* reworked screen color management (softproof, gamut check etc.)
* removed dependency on libraw
* removed dependency on libsquish (solves patent issues as a side effect)
* unbundled pugixml, osm-gps-map and colord-gtk
* text watermarks
* color reconstruction module
* raw black/white point module
* delete/trash feature
* addition to shadows&highlights
* more proper Kelvin temperature, fine-tuning preset interpolation in WB iop
* noiseprofiles are in external JSON file now
* monochrome raw demosaicing (not sure whether it will stay for release, like Deflicker, but hopefully it will stay)
* aspect ratios for crop&rotate can be added to conf (ae36f035e1496b8b8befeb74ce81edf3be588801)
* navigating lighttable with arrow keys and space/enter
* pdf export -- some changes might happen there still
* brush size/hardness/opacity have key accels
* the facebook login procedure is a little different now
* export can upscale
* we no longer drop history entries above the selected one when leaving dr or switching images
* text/font/color in watermarks
* image information now supports gps altitude
* allow adding tone- and basecurve nodes with ctrl-click
* new "mode" parameter in the export panel
* high quality export now downsamples before watermark and frame to guarantee consistent results
* lua scripts can now add UI elements to the lighttable view (buttons, sliders etc...)
* a new repository for external lua scripts was started.


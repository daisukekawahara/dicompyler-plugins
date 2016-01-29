# Introduction #

The GFOVswitch plugin can be used to correct patient studies which contain RTDose files with a Type B(Absolute) Grid Frame Offset Vector. Currently, Dicompyler only allows Type A offset vectors. The plugin acts to switch between Type A(Relative) and Type B(Absolute) offset vectors for use with positioning the dose images.

# Details #

## Usage ##

Once a Dicom RT-Dose object has been loaded you can select GFOVswitch from the drop down plugin menu. The Grid Frame Offset Vector will be switch between Type A(Relative) and Type B(Absolute) and then broadcast the modified RT Dose file.

## 4.Legal ##

Copyright (c) 2012 [Derek M. Tishler](http://www.derektishler.com) and the dicompyler contributors.

All rights reserved, released under a BSD license.
See the file license.txt available at:
> http://code.google.com/p/dicompyler-plugins/source/browse/plugins/GFOVswitch/license.txt
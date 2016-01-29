# 1.Introduction #
## Purpose ##
Allow researchers performing medical simulations using GEANT4 or GAMOS to visualize dose images and DVH associated with DICOM phantom geometries.

Example of dicomplyer's features using data generated from GAMOS(GEANT4):
![http://derektishler.com/g4screen.jpg](http://derektishler.com/g4screen.jpg)


## About ##
The G4 RT-Dose plugin allows the user to view results from a GEANT4 or GAMOS DICOM simulation. It utilizes, from either simulator, the output of the dose per particle scoring and creates RT objects for use in dicompyler.

Currently two printers are supported:

**GmPSPrinter3ddose printer**: the outputted 3ddose.out file containing dose per particle for each voxel is loaded into a 3D array and saved to a RT-Dose object. This file follows a DOSXYZ 3D Dose Data format which can be utilized in other RT viewers. The specifications of this format [can be found here](http://irs.inms.nrc.ca/software/beamnrc/documentation/statdose/node11.html).

**GmPSPrinterG4cout printer**: allows the user to load a file which contains console output of flattened voxel id's and dose scoring. Whether in the gamos.log or a dedicated file, the GmPSPrinterG4cout must be in a form resembling:
```
...
MultiFunctionalDet: SCORER_PARAMETERS
 PrimitiveScorer: SCORER_NAME
 Number of entries= 337261
  index: 31  = 1.06192e-13 Gy
  index: 46  = 1.15505e-13 Gy
  ...
  index: 1228752  = 4.57528e-14 Gy
doseScorer SUM ALL: 3.46296e-07 +/- 0 Gy 
...
```
You may also load a file containing a 2xN table containing only the ID and Dose numbers(such as the Dicom.out file produced by the GEANT4 DICOM example).


# 2.Details #

## Usage ##
Open the patient by selecting the same study that was used in the DICOM simulation. Once the patient has been loaded, the option "G4 RT-Dose..." will appear in the tools menu. A dialog will appear requesting the dose file. The printer will be determined automatically. If the GmPSPrinterG4cout printer is used then the Data.dat file containing compression info will be required unless it is located in the dose file's directory.

The dose data is re-scaled before loading to avoid problems in DVH generation. You may enter a new max value in Gy or press Cancel to avoid scaling.

**Due to [Issue 72](http://code.google.com/p/dicompyler/issues/detail?id=72) the use of the DVH feature requires using the plugin with a study already containing RT struct,dose, and plan files. Load such a patient to activate the DVH plugin which can then be combined with simulation data.**

Upon completion, you may begin selecting contours for viewing from the Isodoses tab.

By default the example GEANT4 folder is located in:
> "(GEANT4)/examples/extended/medical/DICOM"

Test files can be found in the [plugin directory](http://code.google.com/p/dicompyler-plugins/source/browse/#hg%2Fplugins%2Fg4dose).

## Requirements ##

Users working with GEANT4 or the GmPSPrinterG4cout printer will require the file containing compression information for building the patient geometry. This file must be selected if it is not located within the dose file's directory.
|**Required File**|**description**|
|:----------------|:--------------|
|Dose File        |Flattened voxel id & dose (see above for format)|
|Data.dat         |Compression information for DICOM simulation|

Or, if GmPSPrinter3ddose is used:

|**Required  File**|**description**|
|:-----------------|:--------------|
|Dose File         |Output file containing DOSXYZ format|

## Technical ##
  * Compression value error: Your simulator has not rebuilt the binary files generated from the .dcm files. This means that your compression value in Data.dat does not match that of the geometry files created by the DICOM handler in GEANT4. For example, in the 9.4 release c=8 but the binary files have c=4. This problem exists because GEANT4 DICOM checks for existing parsed DICOM files and skips re-creating them if they are found.
  * Simulations with small run sizes will produce images with sparse dose data. Keep in mind data represents dose per particle and any single particle tracks will be well below the 30% contour threshold.
  * GEANT4 DICOM v9.4 example contains a setup that places the beam normal to the slices. To place the beam over the patient change the particles position and direction in DicomPrimaryGeneratorAction.cc back to something like:
```
G4ThreeVector dir(0,1,0);
dir /= dir.mag();
particleGun->SetParticlePosition(G4ThreeVector(0.,-99.9*cm,87.5*mm));
```

# 3.Development #

G4 RT-Dose plugin is in alpha.

> Planned improvements:
    * GUI improvements for simulation browsing/rx dose selection.
    * Correct problem with exporting RT Dose.

Please check back soon.

# 4.Legal #

Copyright (c) 2011-2012 [Derek M. Tishler](http://www.derektishler.com), Brian P. Tonner, and the dicompyler contributors.

All rights reserved, released under a BSD license.
See the file license.txt available at:
> http://code.google.com/p/dicompyler-plugins/source/browse/plugins/g4dose/license.txt
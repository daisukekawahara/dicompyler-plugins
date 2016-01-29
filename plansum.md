# Introduction #

The plansum plugin allows the user to select a DICOM RT-Dose object and add it to the currently loaded RT-Dose.  The result is a 3D dose object containing the summed dose in the region of overlap for the two objects.  Multiple objects can be summed by adding them together one at a time.

# Details #

## Usage ##

Once a Dicom RT-Dose object has been loaded, along with its corresponding RT-Plan, the option "Sum RT Dose..." will become available under the Tools menu.  Selecting this option will bring up the Open Patient dialog again.  Select the RT-Dose object you wish to add to the current object.  If the two Dose objects are from a common CT image set (the SeriesInstanceUID DICOM tag is the same for both), the plugin will calculate their sum and load it into dicompyler.  The prescription dose will be updated to be the sum of the prescription doses for both objects.

## Technical Details ##

Dose data will only be calculated in the region of overlap of the two data sets.  The spatial resolution will be set in each direction to the coarser of the two objects.  For example, adding one object with a voxel size of (1, 1, 2.5) and another with a voxel size of (2, 2, 1) will create an object with voxel size (2, 2, 2.5).

If the two RT-Dose objects overlay exactly and have the same spatial resolution, they will be directly summed.  Otherwise, both of the data sets will have to be interpolated.  This can be a very time consuming process.  If you are running dicompyler from source, you can install [SciPy](http://www.scipy.org/Download) to speed things up.



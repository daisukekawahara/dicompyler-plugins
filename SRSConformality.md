# Introduction #

Used to calculate how well an isodose line from a DICOM RT-Dose object conforms to a selected DICOM RT-Structure.

![http://i.imgur.com/5dNGb.png](http://i.imgur.com/5dNGb.png)

# Details #

Read "A simple scoring ratio to index the conformity of radiosurgical
treatment plans" by Ian Paddick.
J Neurosurg (Suppl 3) 93:219-222, 2000

The SRS Conformality plugin allows the user to select a DICOM RT-Structure object from the currently checked structure list.  Once a structure is checked, the plugin will enable an isodose level to be selected.  From the isodose level selected, the plugin will take the associated RT-Dose object and apply the isodose level as a lower threshold.  The plugin calculates Conformity Index, Underdose Ratio, and Overdose Ratio.

The SRSConformality folder should be placed in the baseplugins directory.

# Goals #

For efficiency reasons would like to change how the plugin finds the selected structure volume (ccs), instead of using CalculateVolume().  Also, the result of recalculating the volume is that there is a rounding of the number.

Would like to validate the accuracy of the conformity percentages (other TPSes, in addition to Eclipse).
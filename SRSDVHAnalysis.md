# Introduction #

[AAPM Task Group 101](http://aapm.org/pubs/reports/RPT_101.pdf) recommended dose limits for stereotactic external photon radiotherapy.  This plugin attempts to provide a second check of a plan (that has already been visually inspected by a Medical Physicist or Dosimetrist) against these dose limits.

![http://i.imgur.com/JkUd9ZD.png](http://i.imgur.com/JkUd9ZD.png)

# Details #

The Analysis folder should be placed in the baseplugins directory. The plugin requires at a minimum a RTSS and RTDOSE to be used.  It takes the volume or dose limits from TG-101 and looks up the corresponding plan value in the DVH (for the parallel structures, it  compares a minimum critical volume below threshold per TG-101).  Currently there is only a pop-up panel that temporarily stores the comparison, but a report feature may be added later.
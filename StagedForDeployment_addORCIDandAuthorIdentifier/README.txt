This folder contains a form used with development of institutional repository functionality.

Full MODS:

The starting point is the Full MODS form deployed to production Islandora sites in September 2016.

This form adds to author information a place for storing an identifier on the author.  In the MODS, this is stored in <name type="personal"><nameIdentifier>. (This MODS field is used to link to an identifier in the MADS on scholar Person Entities, and in the MADS the type can be "ORCID" or "local".)


Deployment log:

As of Oct. 19, 2016, this form is on:
ir-test
fsu-test
fau-test
fgcu-test
ucf-test

- Before copying across test sites, the forms.pl script needs to be updated like so:
-- Needs added to line 35: “ucf”, “valencia”, and “fscj”.
-- Then in the description at lines 71 to 92 of what the script is doing, it should get added that it’s changing all these:  fiu-test , fscj-test , irsc-test , lssc-test , scf-test , spc-test , unf-test , usf-test , uwf-test , and valencia-test .
- Not yet deployed on production sites.
- Before copying across production sites, the forms.pl script needs to be updated like so:
-- Needs added to line 35:  "floradora" and "valencia"
-- Lines 76 - 80 need to be rewritten to have a list of current production sites.
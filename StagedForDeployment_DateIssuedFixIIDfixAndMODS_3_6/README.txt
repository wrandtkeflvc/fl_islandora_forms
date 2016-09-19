This folder contains an in progress form.

Full MODS:

The starting  point is a Full MODS form developed in Aug/Sept. 2016 to corrected a problem with editing records where there is a dateIssued with both a start point and an end point.

Completed development is to:
Combine in the fix to flipping blank type identifiers to type="IID"

The in progress development is to:
Combine in Lydia's updates to be compatible with MODS 3.6.  (I was not able to find this, so there might not be any changes to the Full MODS form. - wvr)

Testing is completed as of Sept. 15, 2016.


MODS Simple Entry:

The starting point is the MODS Simple Entry form deployed in Nov. 2015 on Islandora sites.

Completed development is to:
Combine in the fix to flipping blank type identifiers to type="IID"
and
Combine in Lydia's updates to be compatible with MODS 3.6.

All the changes have been made.

As of Sept. 15, 2016, MODS Simple Entry IID 3_6.xml has been tested and is fine to use on Islandora sites.


Deployment log:

- Sept. 19, 2016:  Wilehlmina installed this on islandora-dev , and on islandora-test.  Gail Lewis will add a code change there to require that the form with element name "id_otheridentifiers" not have any identifiers with type="IID" in it, and give an error message on saving if one is found.
- Not yet deployed on production sites.
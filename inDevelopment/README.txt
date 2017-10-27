accessConditionFormWithRightsstatements_org_AndCreativeCommons.xml
form with open uncontrolled copyright statements, and rightsstatements.org copyright statements, and Creative Commons copyright statements from the same record all in the appropriate field.

The fix that needs to be done on this is:
At this time, the xlink and the human readable value are separately entered.  Those should be coupled together.


FullMODS_fixingPURLtoNotAPURLflipOnOpen.xml

The Full MODS form has a bug to where when it is used to open a PURL, it will flip the value to "Not a PURL".

MODS Simple Entry and Full MODS handle locDispLabel differently. It looks like this was changed sometime between when Priscilla Caplan shared a version of the Full MODS form on a listserv in March 2014 and when Mike Demers installed the Full MODS form in November 2015.

Since MODS Simple Entry is handling this field correctly, it's good to look at this different and get Full MODS form to where it's handling things more like MODS Simple Entry.
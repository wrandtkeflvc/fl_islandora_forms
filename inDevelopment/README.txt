accessConditionFormWithRightsstatements_org_AndCreativeCommons_URIasValue_displayLabel.xml

Just the accessCondition fields and the bare minimum of required fields.  This stores the URI for RightsStatements.org or for Creative Commons as the value of the accessCondition element and uses a displayLabel attribute to separate off RightsStatements.org values and Creative Commons values from uncontrolled values.
Changes needed:  The "use and reproduction" and displayLabel fields are shown to users.  Those should be hidden to make the form visually shorter.  Users can't change those values, so no need to see them (or they should see them in an intentional way like a caption or title or something similar).

(Short form with just required fields and accessCondition;  Development is complete on this, but it can be deployed on sites for a clean up project as needed.)




FullMODS_fixingPURLtoNotAPURLflipOnOpen.xml

The Full MODS form has a bug to where when it is used to open a PURL, it will flip the value to "Not a PURL".

MODS Simple Entry and Full MODS handle locDispLabel differently. It looks like this was changed sometime between when Priscilla Caplan shared a version of the Full MODS form on a listserv in March 2014 and when Mike Demers installed the Full MODS form in November 2015.

Since MODS Simple Entry is handling this field correctly, it's good to look at this different and get Full MODS form to where it's handling things more like MODS Simple Entry.





FullMODS_separtingPURLfromOtherLocationInfo.xml

This is something like a perfect fix to the PURL / URL problem in terms of editing MODS.  The problem is that some PURLs on any given site will be in the institution's PURL area and some will be in FCLA's PURL area.  So, this cannot necessarily be used to fix a record where the PURL was flipped - it can't be used if the PURL that is incorrectly as a URL is in FCLA's PURL area.




JustTheLocationFieldMixOfMODSsimpleEntryAndFullMODSform.xml

This is an improved <location> field for the Full MODS form.  The CRUD for displayLabel="PURL" is corrected in this form.  This was installed on FAU's production site on Oct. 8, 2018 for clean up of affected records (and FAU instructed to look closely at how this form is working and report problems or unexpected behavior.  (One change made to the delete field after it was installed on FAU's site.)




MODSsimpleEntry_separatingPURL_from_physicalLocation_from_URLs.xml
FullMODS_separatingPURL_from_physicalLocation_from_URLs.xml

Buggy as of Oct. 2018 (opens the same <location> instance in different fields).
Goal is to separate PURL from URL from all location info.  This is because logically a URL for a resource can never be the same location as the physical location.  So those should happen in two separate <location> elements, not within a single <location> element.
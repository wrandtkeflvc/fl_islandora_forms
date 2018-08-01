A template can be installed on a form association.

------------------------------------------------------------------
Instructions for installing a template on an FLVC Islandora site
------------------------------------------------------------------

1) Make a new item of the same kind that you want to make a template for.  Common uses of templates are to autofill info for every article in a Serial or to autofill fields for each Newspaper Issue in a single Newspaper.

2) Edit the MODS for that sample object, and get the standard metadata fields that you want autofilled to all look perfect.  Do not fill in any fields unless you want them autofilled.  You will use the MODS record from this item to make the template.  (The MODS forms will make you have a title, an IID, and maybe a date created, so you are stuck with those.)

3)  Download the MODS for that object.  Click to the object, click to the "Manage" tab, click to the "Datastreams" tab, click to "export" the MODS.

4)  Manually delete the following fields:
* Delete the <identifier type="IID"> field.
* Delete the <location displayLabel="purl"><url> field.
* Consider deleting the <titleInfo><title> field.  This is an FLVC required field.  You might want it in your template, but you might not.
* Consider deleting the <dateIssued> (might be <dateIssued encoding="w3cdtf"> ) field.  This is a required field for the Newspaper Issue content model. You might want it in your template, but you might not.

5)  Rename that file to indicate that it's your template.

6)  Validate the XML template.  Oxygen XML Editor is a good tool to use for this, because this will validate against the MODS schema referenced in the header.

7)  On the Islandora site that you will install the template on, go to the "Form Builder" section.  Copy either the MODS Simple Entry form or the Full MODS form, and title your copy to be either "MODS Simple Entry (name of the collection/serial/newspaper your template is for)" or "Full MODS (name of the collection/serial/newspaper your template is for)".

8)  Make a checklist of content models that you will use this form with.  It might be all kinds of media, or it might be for Newspaper Issue only.  (Articles in a Serial are the PDF content model.)

9)  Click back to the "Form Builder" section.  On the form you just created, click to "Associate".  Refer to your list of content models you will use this form with.  Add the form associations according to the screenshots in the home directory of this git repository, but for the last configuration step on the form association, upload your .xml template.

10)  Test out the template.  For each content model you will use the template with, create an object, select the new form you created and installed the template on, look at the autofilled form fields and make sure they look OK.  Now, fill in any required fields (like IID), and create the item.  Click to the "Manage" tab, then to "Datastreams", then "download" the MODS record.  Validate it on your desktop and look over it to make sure that all the info you want is in the template and no extra info is in the template.

11)  Email to the library that the template is installed and ask them to check it out.

12)  Either add the template to this git repository in the /templates/ directory (match file naming conventions and update /templates/README.txt ), or if you do not have permissions or are not comfortable with git, then email the template on the FLVC Islandora Developers listserv and make sure to include both the .xml template and a description of what the template is and how it will be used.

----------------------------------------------------------------------------------------------------------
Here's a list of templates which FLVC has installed on Islandora sites, and background on each template.
----------------------------------------------------------------------------------------------------------

----
FSJC
----

template_fscj_2017Oct_CampusVoice.xml
Installed on FSCJ's site in October 2017.

RETIRED template_fscj_2017Oct_Kalliope.xml RETIRED
Installed on FSCJ's site in October 2017 for the serials.  Installed in December 2017 for the Newspaper Issue Content Model.  From Dec. 12 to 19, 2017, the form association did not include the MODS to DC transformation.
Retired Aug. 1, 2018.

template_fscj_2018Aug_Kalliope.xml
Installed Aug. 1, 2018.

template_fscj_2018spring_WorthQuoting
Installed April 2018 on FSCJ's production site (installed on production before being installed on test).
RightsStatements.org value added Aug. 1, 2018.

template_fscj_2018spring_WriterToWriter
Installed April 2018 on FSCJ's production site (installed on production before being installed on test).
RightsStatements.org value added Aug. 1, 2018.

template_fscj_2018summer_Alpha.xml
Installed July 2018 on fscj-test .
RightsStatements.org value added Aug. 1, 2018.

template_fscj_2018summer_Experience.xml
Installed July 2018 on fscj-test .
RightsStatements.org value added Aug. 1, 2018.

---
FSU
---

template_fsu_circa2014_FullMODS_Flambeau.xml
Installed on FSU's site.  There is a duplicate Full MODS form named "Full MODS_Flambeau".  That form is associated with the PDF content model, and this template is installed on that association.

template_fsu_circa2015_FullMODS_secolo.xml
Installed on FSU's site.  There is a duplicate Full MODS form named "Full MODS_secolo".  In 2016, this template was associated with the PDF content model.  As of 2018, this template is retired.

template_fsu_circa2016_FullMODS_GirlsOwnAnnual.xml
Installed on FSU's site.  There is a duplicate Full MODS form named "Full MODS_GirlsOwnAnnual".  That form is associated with the PDF content model, and this template is installed on that association.
In 2016, this template was associated with the PDF content model.  In 2017/2018, this template was installed on rootSerialCModel and on intermediateCModel .

---
UCF
---

ucf_circa2014FHQFullMODS.xml
Installed on UCF's site.  There is a duplicate Full MODS form named "Full MODS - FHQ".  That form is associated with the PDF content model only, and this template is installed on that association.
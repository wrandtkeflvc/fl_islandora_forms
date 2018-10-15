==================
fl_islandora_forms
==================

Background information on this repo:

The Islandora XML Form Builder allows creation of forms to allow data to be entered and stored as XML.  The interface is similar to Drupal's Form Builder, but Islandora XML Form Builder specifically accounts for xpath to retrieve and store information as XML.  Islandora Form Builder also allows each data entry form to be exported as XML, and imported into other sites.

The files in this repo are exports of forms in use for metadata entry on Florida Islandora sites.  (FLVC has a local MODS profile, which is provided at the end of this README.)

Forms in the top level directory are the working forms.  Commit messages should give the reason for a commit (usually an ISG recommendation or an update to new version of MODS).  Forms in /pastDeployments/ are versions of forms made at the date of release.  This allows a quick glimpse into the history of form deployments on production Islandora sites.


---(1) MODS Simple Entry.xml---
One of the two forms which is enabled for all content models (other than the Collection Content Model) on Florida Islandora sites.

---(2) Full MODS.xml---
One of the two forms which is enabled for all content models (other than the Collection Content Model) on Florida Islandora sites. It does not have all MODS fields, but does have many of them.  The form is designed for the use case of someone needing to edit a MODS datastream when that datastream contains a less-used field.

---(3) Full MODS Newspaper Issue.xml---
Full MODS customized for newspaper entry.  This was deployed across Florida Islandora sites in early November 2015, and is associated only with the Newspaper Issue Content Model.  The purpose of this separate form is to require a date be entered for each newspaper Issue.  A date is required in order for the issues to display correctly within the larger Newspaper object.
On each new deployment of a MODS form, the Full MODS Newspaper Issue form should be recreated by taking a Full MODS form and making the date a required field.

---(4) Collection Form FL-Islandora.xml---
Enabled for the Collection Content Model on Florida Islandora sites.  It contains only a few fields (Title, Description, Note, and Language).

General note on MODS form associations:
This repo has screenshots of MODS form associations for each form that must be implemented through the GUI.
The transform mods_to_dc.xsl is versioned at https://github.com/FLVC/islandora_xml_forms/tree/flvc/builder/transforms/mods_to_dc.xsl
The transform FLVC_MODS_postprocessing.xsl is versioned at https://github.com/FLVC/islandora_xml_forms/tree/flvc/builder/self_transforms/FLVC_MODS_postprocessing.xsl

---/drafts/DC-Tagged MODS.xml---
Dublin Core labeled fields mapped to MODS.  This is not deployed on Florida Islandora sites at this time.


How Florida Islandora deploys a new form across about 20 sites:  Once a form (or a new version of a form) is finalized on the development server, that form is installed to the test server (islandora-test) and form associations are set up and tested.  Then a forms.pl script is run which updates the form across Islandora test sites.  Then, the flvc:owningInstitution is set to autopopulate in each form (forms.pl updates all three forms even if only one changed).  Then that form is installed on a production site (floradora) and form assocations are set up and tested.  Then a forms.pl script is run which updates the forms across the Islandora production sites.  Then, the flvc:owningInstitution is set to autopopulate in each form (forms.pl updates all three forms even if only one changed).


=========================================================================
Background information on how Florida Islandora is using Islandora Forms:
========================================================================= 

Florida Islandora is a large consortial system used by public universities and colleges in Florida.  Each university or college with a site has it's own Drupal front end, and sites share a Fedora Commons install.

All Built-In MODS form associations are disabled on Florida Islandora sites.

Then two forms are enabled for all content models:  (1) Full MODS and (2) MODS Simple Entry.  Additionally, a third (3) Collection Form FL-Islandora form is enabled for collection content model objects starting with Islandora version 7.x-1.6 (first version of Islandora to allow MODS to be stored with a collection level object).

On upload, users see the MARCXML upload screen.  Next they get a screen where they have a drop down menu to choose “Simple MODS” (the default selection) or “Full MODS”.  Then they click OK and go to the form they chose.

The Full MODS form has many (but not all) fields that are available in MODS.  Updates to the form are made when a new version of MODS is released by the Library of Congress, or as interface changes are recommended by Florida's Islandora User Group (ISG).

The MODS Simple Entry form has a few fields, and provides a less lengthy entry form for workflows where someone is creating metadata.

On initially uploading an object to Islandora, users have the opportunity to upload a MARC record which will be crosswalked to and stored as a MODS datastream.  Users can later update the MODS datastream using the Full MODS form.  What is different from a basic Islandora install is that the Full MODS form allows touch ups to metadata that came in through a MARC record and crosswalked to MODS.  With a basic Islandora install, a user would only be able to edit the handful of fields available in the default MODS edit form for that content model.

Florida State University is a development partner.  Their metadata librarian does MODS form work as well.  The FSU Libraries github is at https://github.com/fsulib/ and FSU's metadata librarian's github is at https://github.com/mrmiguez .

For instructions on using templates with Islandora forms, refer to the README in the /templates/ directory of this repo.


=======================================================
Step-by-step Instructions for FLVC on installing a form
=======================================================

1)  Delete the form off one site, and reinstall the new version of that form.  For upadtes on test sites, tend to use islandora-test.  For updates on production sites, tend to use floradora.

2)  To install the form:  delete the old form, then import the new form, then work through building all the form associations using the screenshot of the form associations.

3)  Run the forms.pl script to copy over the form from the site you installed on to all other sites.  This is in /usr/local/islandora/forms/ and to run, you type "./forms.pl test" for islandora-test or "./forms.pl floradora" for floradora.  (Also, check the source code of the forms.pl script and ensure that all sites are list.  When you check, you are pretty much checking to ensure that any newly launched sites have been added.)

4)  Click into FSU's production site, and remove the fields of each form that are interacting with the RightsStatements.org and Creative Commons controlled statements.  FSU is doing these with an xlink attribute.  So, FLVC's default forms will not work with FSU's metadata profile and will instead remove the values from the metadata.

5)  Click to each site, and edit the form in Form Builder.  Make the default Owning Institution value match the value of the college/university on a Create.  (After you "Save & Preview", you will see that the default drop down option matches your current college/university, and that's how you know you've correctly entered the Create value.)


=========================
FLVC's local MODS profile
=========================

<identifier type="IID">
- Required
- non-repeatable
- Each IID must be unique from all other IIDs used across institutions.
- Requirements: The only characters allowed are A to Z, a to z, 0 to 9, underscore, dash, period, left- and right-parenthesis. (This requirement is because the IIDs are used to make PURLs.)
- Requirements: No spaces allowed in an IID. (This requirement is because the IIDs are used to make PURLs.)

<titleInfo><title>
- Required (This is a required field in all forms.)

<originInfo><dateIssued>
- The dateIssued is required for Newspaper Issues in order to show up in the tree browse from the top level newspaper element.
- A dateIssued is also required by the Excel to MODS Transformer service. The Excel to MODS Transformer will not process MODS unless a dateIssued is included.

Local fields: These are <flvc:flvc><flvc:owningInstitution></flvc:owningInstitution><flvc:submittingInstitution></flvc:submittingInstitution><flvc:otherLogo></flvc:otherLogo><flvc:objectHistory></flvc:objectHistory></flvc:flvc>

<flvc:owningInstitution>
- Required
- non-repeatable
- "The institution that owns the digital object." (text FLVC displays in the MODS forms)
Pulls from a controlled vocabulary (because it is used for creating a PURL based on FLVC's code for the owning institution and IID). This is implemented with a drop down menu in forms.

<flvc:submittingInstitution>
- optional field
- non-repeatable
- "The institution submitting the digital object for ingest." (text FLVC displays in the MODS forms)
- Pulls from the same controlled vocabulary as <flvc:owningInstitution>.

<flvc:otherLogo>
- optional field
- repeatable (according to http://wiki.fcla.edu/wiki/index.php/DL:Offline_Ingest_Specs )
- "The name of a logo to display with the object in addition to the logo of the owning institution." (text FLVC displays in the MODS forms)

<flvc:objectHistory source="digitool">
- optional field
- Used to store provenance information about Digitool.
- Required that one and only one FLVC <extension> exists.
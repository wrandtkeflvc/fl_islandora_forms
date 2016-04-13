fl_islandora_forms
================================

Background information on this repo:

The Islandora XML Form Builder allows creation of forms to allow data to be entered and stored as XML.  The interface is similar to Drupal's Form Builder, but Islandora XML Form Builder specifically accounts for xpath to retrieve and store information as XML.  Islandora Form Builder also allows each data entry form to be exported as XML, and imported into other sites.

The files in this repo are exports of forms in use for metadata entry on Florida Islandora sites.

Forms in the top level directory are the working forms.  Commit messages should give the reason for a commit (usually an ISG recommendation or an update to new version of MODS).  Forms in /pastDeployments/ are versions of forms made at the date of release.  This allows a quick glimpse into the history of form deployments on production Islandora sites.


---MODS Simple Entry---
One of the two forms which is enabled for all content models (other than the Collection Content Model) on Florida Islandora sites.

---Full MODS---
One of the two forms which is enabled for all content models (other than the Collection Content Model) on Florida Islandora sites. It does not have all MODS fields, but does have many of them.  The form is designed for the use case of someone needing to edit a MODS datastream when that datastream contains a less-used field.

---Collection Form FL-Islandora---
Enabled for the Collection Content Model on Florida Islandora sites.  It contains only a few fields (Title, Description, Note, and Language).

---Full Mods_Newspaper---
Full MODS customized for newspaper entry.  This was deployed across Florida Islandora sites in early November 2015, and is associated only with the Newspaper Issue Content Model.  The purpose of this separate form is to require a date be entered for each newspaper Issue.  A date is required in order for the issues to display correctly within the larger Newspaper object.


---/drafts/DC-Tagged MODS.xml---
Dublin Core labeled fields mapped to MODS.  This is not deployed on Florida Islandora sites at this time.


Background information on how Florida Islandora is using Islandora Forms: 

Florida Islandora is a large consortial system used by public universities and colleges in Florida.  Each university or college with a site has it's own Drupal front end, and sites share a Fedora Commons install.

All Built-In MODS form associations are disabled on Florida Islandora sites.

Then two forms are enabled for all content models:  (1) Full MODS and (2) MODS Simple Entry.  Additionally, a third (3) Collection Form FL-Islandora form is enabled for collection content model objects starting with Islandora version 7.x-1.6 (first version of Islandora to allow MODS to be stored with a collection level object).

On upload, users see the MARCXML upload screen.  Next they get a screen where they have a drop down menu to choose “Simple MODS” (the default selection) or “Full MODS”.  Then they click OK and go to the form they chose.

The Full MODS form has many (but not all) fields that are available in MODS.  Updates to the form are made when a new version of MODS is released by the Library of Congress, or as interface changes are recommended by Florida's Islandora User Group (ISG).

The MODS Simple Entry form has a few fields, and provides a less lengthy entry form for workflows where someone is creating metadata.

On initially uploading an object to Islandora, users have the opportunity to upload a MARC record which will be crosswalked to and stored as a MODS datastream.  Users can later update the MODS datastream using the Full MODS form.  What is different from a basic Islandora install is that the Full MODS form allows touch ups to metadata that came in through a MARC record and crosswalked to MODS.  With a basic Islandora install, a user would only be able to edit the handful of fields available in the default MODS edit form for that content model.

Florida State University is a development partner.  Their metadata librarian does MODS form work as well.  The FSU Libraries github is at https://github.com/fsulib/ and FSU's metadata librarian's github is at https://github.com/mrmiguez .
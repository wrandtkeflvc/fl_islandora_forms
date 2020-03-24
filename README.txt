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

1)  Delete the form off one site, and reinstall the new version of that form.  For updates on test sites, tend to use islandora-test.  For updates on production sites, tend to use floradora.

2)  To install the form:  delete the old form, then import the new form, then work through building all the form associations using the screenshot of the form associations.

3)  Run the forms.pl script to copy over the form from the site you installed on to all other sites.  This is in /usr/local/islandora/forms/ and to run, you type "./forms.pl test" for islandora-test or "./forms.pl floradora" for floradora.  (Also, check the source code of the forms.pl script and ensure that all sites are list.  When you check, you are pretty much checking to ensure that any newly launched sites have been added.)

4)  Click into FSU's production site, and remove the fields of each form that are interacting with the RightsStatements.org and Creative Commons controlled statements.  FSU is doing these with an xlink attribute.  So, FLVC's default forms will not work with FSU's metadata profile and will instead remove the values from the metadata.

5)  Click to each site, and edit the form in Form Builder.  Make the default Owning Institution value match the value of the college/university on a Create.  (After you "Save & Preview", you will see that the default drop down option matches your current college/university, and that's how you know you've correctly entered the Create value.)

6)  Maintain documentation on the history of the forms in this git log.
    The /inDevelopment/ directory contains in development forms and a README.txt file which should have information about the goals each form is attempting to accomplish, whether or not it's been tested, known bugs, or whether it's ready to deploy.
    When you deploy a form on production, update the cannonical forms in the top level of this git repository.  Also, spin off a copy to /pastDeployments/ .  Include the date of the deployment on production in the form name, and include a short summary of the change in the commit message.


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

How to Store Digital Object Identifiers in the MODS
Digital Object Identifiers (DOIs) should be stored in MODS in the identifier element with a type="doi".

Example:

<identifier type="doi">10.1007/BF02126356</identifier>

and you enter it in the MODS form like this:

Screenshot of a DOI entered into the MODS form.  Under the header "Identifiers", for "Type" enter "doi" (all lowercase), and for "Identifier" enter the DOI only and not any URL made from the DOI.  For example, enter "10.1007/BF02126356" as the "Identifier".

The DOI encoding is used to pull any altmetrics information available for the publication in the altmetric.com service. For this to work, the DOI has to be stored exactly as described above.

How to Store RightsStatements.org values in the MODS
RightsStatements.org values should be entered into the MODS in the accessCondition element with a type="use and reproduction" and with a displayLabel="RightsStatements.org". The URI should be entered with no other information in the same field (ie. do not mix in human readable information along with the URI - the URI should be by itself).

Significantly, RightsStatements.org URIs use "http" and NOT "https".

Example:

<accessCondition type="use and reproduction" displayLabel="RightsStatements.org">http://rightsstatements.org/vocab/InC/1.0/</accessCondition>

and you enter it in the MODS form like this:

Screenshot of the RightsStatements.org field in the MODS form.  Under the header "ACCESS CONDITION: RIGHTSSTATEMENTS" then under the header "RightsStatements.orgValue", use the drop down menu to select a statement.  You will see a human readable value in the form, and the form will save that as a URI.


RightsStatements.org and the Excel to MODS Transformer

As of summer 2018, the Excel to MODS Transformer cannot create RightsStatements.org values encoded to FLVC's requirements. There are no plans to add this functionality. If you wish to use the Excel to MODS Transformer to create metadata, then enter the RightsStatements.org URIs in the column labeled "access condition" (just a single URI for each file with no other info in that "access condition" column). Then contact help@flvc.org with "Islandora" in the subject line, send the Excel file, and request FLVC to send you back a .zip file of the MODS records with the RightsStatements.org encoding.


Special note on encoding RightsStatements.org as an xlink:

FLVC is aware that FSU will encode the RightsStatements.org values as an xlink.


Special note about the Digital Public Library of America's (DPLA's) MODS requirements:

The DPLA has examples of how to encode RightsStatements.org in this guidance document Standardized Rights Statements Implementation Guidelines. DPLA requires that a RightsStatement.org or Creative Commons value be included with every item going into DPLA. And, DPLA requires that this RightsStatement.org or Creative Commons value be the only value stored in <accessCondition type="use and reproduction"> and that local rights statements using uncontrolled language be stored using another type, type="local rights statement". However, this is incompatible with the MODS schema. The examples in the User Guidelines clearly show uncontrolled rights statements in type="use and reproduction". Because the Library of Congress maintains the MODS standard, FLVC will follow the published standard. DPLA is one of many projects using the MODS standard and is not authoritative.

Islandora shares out records via OAI-PMH. One of the settings on the OAI-PMH configuration in Islandora is an option to transform records as they go out. It is possible to install a transformation on the Islandora site's OAI-PMH feed which would remove uncontrolled <accessCondition type="use and reproduction"> statements and send out only the RightsStatements.org and Creative Commons values by taking <accessCondition type="use and reproduction" displayLabel="RightsStatements.org"> and converting it to <accessCondition type="use and reproduction">.

How to Store Creative Commons values in the MODS
Creative Commons values should be entered into the MODS in the accessCondition element with a type="use and reproduction" and with a displayLabel="Creative Commons". The URI should be entered with no other information in the same field (ie. do not mix in human readable information along with the URI - the URI should be by itself).

Encoding is identical to that used for RightsStatements.org values, except that for Creative Commons values, the displayLabel attribute is different. diplayLabel="Creative Commons" should be used.

Significantly, Creative Commons URIs use "http" and NOT "https".

How RightsStatements.org and Creative Commons values are used in Islandora
ReuseRightsFacetsScreenshot.png

The RightsStatements.org and Creative Commons values are matched to one of 3 categories:

Free Re-use
Limited Re-use
No Re-use
Here's what's in each

Free Re-use contains:
RightsStatements.org: No Copyright US: http://rightsstatements.org/vocab/NoC-US/1.0/
RightsStatements.org: No Known Copyright: http://rightsstatements.org/vocab/NKC/1.0/
public domain: http://creativecommons.org/publicdomain/mark/1.0/
Creative Commons: CC-BY-SA: http://creativecommons.org/licenses/by-sa/4.0/
Creative Commons: CC-BY: http://creativecommons.org/licenses/by/4.0/
Creative Commons: CC0: http://creativecommons.org/publicdomain/zero/1.0/
Limited Re-use contains:
RightsStatements.org: No Copyright - Non-Commercial Use Only: http://rightsstatements.org/vocab/NoC-NC/1.0/
RightsStatements.org: In Copyright - Educational Use Permitted: http://rightsstatements.org/vocab/InC-EDU/1.0/
RightsStatements.org: In Copyright - Non-Commercial Use Permitted: http://rightsstatements.org/vocab/InC-NC/1.0/
RightsStatements.org: No Copyright - Contractual Restrictions: http://rightsstatements.org/vocab/NoC-CR/1.0/
RightsStatements.org: No Copyright - Other Known Legal Restrictions: http://rightsstatements.org/vocab/NoC-OKLR/1.0/
Creative Commons: CC-BY-NC: http://creativecommons.org/licenses/by-nc/4.0/
Creative Commons: CC-BY-NC-ND: http://creativecommons.org/licenses/by-nc-nd/4.0/
Creative Commons: CC-BY-ND: http://creativecommons.org/licenses/by-nd/4.0/
Creative Commons: CC-BY-NC-SA: http://creativecommons.org/licenses/by-nc-sa/4.0/
No Re-use contains:
RightsStatements.org: Copyright Not Evaluated: http://rightsstatements.org/vocab/CNE/1.0/
RightsStatements.org: Copyright Undetermined: http://rightsstatements.org/vocab/UND/1.0/
RightsStatements.org: In Copyright: http://rightsstatements.org/vocab/InC/1.0/
RightsStatements.org: In Copyright - Rights-holder(s) Unlocatable or Unidentifiable: http://rightsstatements.org/vocab/InC-RUU/1.0/
RightsStatements.org: In Copyright - EU Orphan Work: http://rightsstatements.org/vocab/InC-OW-EU/1.0/
How to Store ORCIDs in the MODS
ORCIDs should be stored in <name><nameIdentifier type="ORCID">.

The ORCID is always the URI version, and should always be expressed with "https" and NOT "http". ORCID's guidance document of the ORCID Identifier states, "The ORCID iD is expressed as an https URI, i.e. the 16-digit identifier is preceded by "https://orcid.org/". A hyphen is inserted every 4 digits of the identifier to aid readability."


For example:


<name>

<namePart type="given">Wilhelmina</namePart>

<namePart type="family">Randtke</namePart>

<nameIdentifier type="orcid">https://orcid.org/0000-0002-7439-8205</nameIdentifier>

</name>


As of summer 2020, Islandora is not interacting with the ORCID API, and adding interaction with the ORCID API is not planned or scheduled.
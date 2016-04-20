Each of these forms:
1) Opens the first occurring IID in a box labeled “IID Identifier” to the user and with $form[‘id’] to the system.
2) Opens all subsequent IIDs and any other identifiers in another box labeled “Other Identifiers” to the user and with $form[‘id_otheridentifiers’] to the system.

The following is implemented programmatically when the form is saved:
It loops through the array $form['id'][$i] checking that at least one has $form['id'][$i]['type'] set to 'IID'.  
Check for bad characters and uniqueness for all $form['id'][$i]['identifier'] with $form['id'][$i]['type']=='IID'.

Currently, it is possible to save multiple IIDs.  A next step is to alter the programmatic check to make it only allow one $form['id'][$i]['type'] of 'IID' and to not allow $form['id_otheridentifier'][$i]['type'] to be 'IID'.
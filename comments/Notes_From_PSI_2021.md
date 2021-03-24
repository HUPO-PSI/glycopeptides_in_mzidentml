# Session 6: Glycoproteomics in mzIdentML and mzTab


## Andy's pre-presentation comments:
Some notes from Andy, which I sent to Joshua just now by email, copied here:

- Is it common to get peptides with and without glycans for a given protocol (I assume so but don’t see this in your example mzid file)?
- Ideally any changes we should make, should be “backwards compatible” with mzid 1.2 i.e. can be accommodated without breaking any cardinalities or mapping rules. Based on a first review, this looks to have been maintained
- A pathway to getting this implemented would be a minor update to mzid 1.2 -> 1.2.1, with PSI document review and an accompanying paper and software support. We should discuss if there are any logistical hurdles to this, but again this seems straightforward.
 
For mzid 1.2, we added a table of “special features” encoded via a CV term:
 
Peptide-level scoring
MS:1002490
Statistics have been performed on non-redundant peptide identifications.
Modification localization scoring
MS:1002491
Scoring has been performed on the sites of peptide modification.
Consensus scoring
MS:1002492
Multiple search engines have been used for peptide identification.
Sample prefractionation
MS:1002493
The file contains the results of merged pre-fractionation analyses.
Cross-linking search
MS:1002494
The search engine has analysed cross-linked (and regular) peptides, using the new encoding described here.
De novo search
MS:1001010
De novo sequencing of peptides has been performed, meaning that 0 . . n relationships from peptides to proteins are allowed (rather than 1 . . n).
Proteogenomics search
MS:1002635
Peptides have been mapped back to genome level coordinates, stored in the file.
Spectral library search
MS:1001031
The identifications have been made by searching against a spectral library. 0 . . n peptides to proteins

 
We may need to add one for a glyco search, but only if there are some details that need to be explicitly checked by the validator, as for the cross-linking search.
I see that you added a term for this during the presentation
 
Updating the validator may be tricky though, since Gerhard Mayer used to do this and has now moved on. I don’t know if anyone else will have the bandwidth to get on top of the Java code for this. One to discuss!
 
====================================================================================

## Further discussion:
Nathan explained more details about GNOME.
For aggregate glycan IDs, composition unknown on two sites, may want to have a local group ID, similar to crosslinking representation, so that it is clear how they pair up, with all mass held on one of the pair.

Seems okay to list all glycans (like a database) in <SearchModification>
Fragmentation mode encoding in mzML or in mzIdentML? This is relatively a small issue. Listing the specific parameter used y the search engine might be enough
Scoring systems: List all of them as CV parameters.
	Name of Software: Name of parameter
It is difficult to agree on common CV parameters between different software. We never got it solved for mzIdentML search engines. 
Solution using searchengine: q-value seems okay, particularly if the CV is well structured with is_a relationships

**ACTION: Joshua to speak to Eric, Yasset and Matt to discuss**

=================

## Validator: Needs to be updated.
Validation needed in the modification element, which is a bit different.

Special scoring  systems/FDR for glycans? Probably not.

Include the GNO ontology.

**ACTION POINTS:**
1. Update the mzIdentML 1.2 to 1.2.1.
2. Adding the glycopeptide centric additions
3. Doing some othe (minor) general updates in other sections
4. Support in search engines? We can try. It would be great to reach out. ProteinMetrics export as the  use case.
5. Monthly call to get this finished?
    1. Email Andy Jones and others to setup times

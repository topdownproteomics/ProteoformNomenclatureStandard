#Proteoform Nomenclature Standard

Authors
* Richard LeDuc, Northwestern University (Chair)
* Veit Schwämmle, University of South Denmark
* Michael Shortreed, University of Wisconsin-Madison
* Anthony Cesnik, University of Wisconsin-Madison
* Stefan Solntsev, University of Wisconsin-Madison
* Jared Shaw, Pacific Northwest National laboratory

## Introduction
This document gives seven rules for writing a fully characterized proteoform. A proteoform is a specific set of amino acids arranged in a particular order, which may be further modified (cotranslationally, posttranslationally or chemically) at designated locations. This nomenclature is intended to be both machine and human readable, and to be sufficiently flexible to meet current and foreseeable needs. Examples and a series of recommended Best Practices are provided.

The notation must:
* Provide an unambiguous way for writing an individual proteoform.
* Be Human readable. Suitable for display in written document or presentation.
* Be Machine parsable. 
* Contain the complete amino acid sequence of the observed proteoform
* Specify the location and type of each modification.

## The Nomenclature
The proposal consists of a series of rules for writing a proteoform sequence with modifications.  The sequence written is the sequence in question, whether observed or hypothesized, as opposed to the canonical sequence. Amino acids not observed are excluded from the nomenclature. For example, N-terminal M cleavages are noted simply by not including the terminal M in the sequence.

### Rule 1
The base sequence of the proteoform is written using the standard capitalized single character amino acid codes. Although ambiguous characters, such as J and X, can be used, no characterized proteoform can contain these symbols.
```
SEQUENCE
SEQUXXCE
```
This is a partially characterized sequence.

### Rule 2
Tags are used to signal information regarding a modification; they are denoted by square brackets. . Tags are placed after the character representing the modified amino acid. Multiple modifications of the same amino acid are described by multiple square bracket pairs.
```
SEQUK[Unimod:Label:13C(3)][Acetyl]ENCE
```

### Rule 3
Tags contain Descriptors that take the form of Key/Value pairs, where the Key and Value are separated by colons. The Key alerts the reader to the type of the descriptor. Some descriptors have implied keys that do not need to be written out, see Rules 5 and 6.
```
SEQUEN[mass:+14.02]CE
```
This is read as a +14.02 Da mass shift on an asparagine residue.

### Rule 4
Multiple descriptors can be placed in a single tag, provided they are separated by pipes.
```
SEQUEN[mod:Methyl|mass:+14.02]CE
```
This is read as a methylation of an asparagine residue, with a mass shift of +14.02 Da.

### Rule 5
The supported descriptors are: Mass, Chemical Formula, Additional Information, Modification Name, and Database Accession. The use of each is detailed below. A key must be present in a descriptor if it is mandatory, and an optional key may be omitted.
#### MASS
Key (Mandatory): mass
Specification: Mass difference in Daltons between the coded amino acid and the observed mass. Can be used to show the location of an unclassified mass shift. Arbitrary precision is allowed, and positive mass shifts can be specified with either a plus sign or no sign. Negative shifts must be specified with a negative sign. The mass is assumed to be observed monoisotopic unless there is an INFO tag (below) explaining otherwise.
```
SEQ[mass:+15.995]UENCE
SEQ[mass:+16]UENCE
SEQ[mass:16]UENCE
```
These three examples could refer to the same proteoform.
#### CHEMICAL FORMULA
Key (Mandatory): formula
Specification: Chemical formulas of modifications may be specified using this descriptor. Formulas must use the UniMod sysmbols provided here: http://www.unimod.org/masses.html, and follow the rules under Composition at http://www.unimod.org/fields.html.
```
SEQUEN[Methyl|formula:H(2)C]CE 
SEQUEN[glucosylgalactosyl|formula:O Hex(2)]CE
```

The subcommittee settled on the use of the UniMod formula format with little discussion. After the final subcommittee meeting it was brought to Rich LeDuc’s attention that the UniMod notation has several flaws, and is not widely used.

It is standard for parenthesis in a chemical formula to indicate multiple identical groups (Source: bottom of Page 20 (32 in the PDF) from IUPAC’s Red Book https://www.iupac.org/cms/wp-content/uploads/2016/07/Red_Book_2005.pdf).
There are many approved usages of parentheses, but elemental stoichiometry isn’t one (https://en.wikipedia.org/wiki/Structural_formula#Condensed_formulas).

The following resources don’t use parentheses in the way Unimod does
   UniProt (http://www.uniprot.org/docs/ptmlist)
   RESID (http://pir.georgetown.edu/cgi-bin/resid?id=AA0001)
   PSI-MOD (http://www.ebi.ac.uk/ols/ontologies/mod/terms?iri=http%3A%2F%2Fpurl.obolibrary.org%2Fobo%2FMOD_00198)
   ChemCalc (http://www.chemcalc.org/)

#### ADDITIONAL INFORMATION
Key (Mandatory): info
Specification: This descriptor is used to signal that unstructured text has been added to the tag. It is expected that this will be used in the development of new descriptors, and is included to allow the maximum utility of this system. Descriptors may not contain the pipe character.

```
SEQ[info: Some comment about this amino acid]UENCE
```
#### MODIFICATION NAME
Key (Optional): mod
Specification: A common name for the modification. The default names are the UniMod Interim Names available here (http://www.unimod.org/modifications_list.php). 
```
SEQUEN[Methyl]CE
```

When specifying a modification using a common name other than the UniMod Interim Name, provide the database name in parentheses.
```
PEPT[Phosphothreonine(UniProt)]IDE
PEPT[O-phospho-L-threonine(RESID)]IDE
PEPT[O-phospho-L-threonine(PSIMod)]IDE
```

The allowed values must come from the following fields:
	Unimod - Interim Name
	UniProt - ID
	RESID - Name
	PSI-MOD - Short label
	BRNO - Common nomenclatures used for histone PTMs (e.g. ph, me1, ac)
#### DATABASE ACCESSION
Key (Mandatory): One of the allowed database names: Unimod, UniProt, RESID, PSI-MOD, UniCarbKB, PROOntology, or BRNO
Specification: This descriptor is used to link the modification to a database entry by means of a database accession number.
```
PEPT[Unimod:21]IDE
PEPT[UniProt:PTM-0254]IDE
PEPT[RESID:AA0038]IDE
PEPT[PSI-MOD:MOD:00047]IDE
```

Comment: There are a number of competing databases which provide both names and accession number for the various modifications that can occur to amino acids. It is not the intention of this protocol to force users to one or another of these databases.
 
Supported PTM databases
Unimod (default) - http://www.unimod.org/modifications_list.php
UniProt (recommended) - http://www.uniprot.org/docs/ptmlist
RESID (recommended) - http://pir.georgetown.edu/resid/resid.shtml
PSI-MOD (recommended) - http://www.ebi.ac.uk/ols/ontologies/mod
BRNO MOD (acceptable)
UniCarbKB (acceptable) - http://www.unicarbkb.org/
PRO Ontology/NCBI  (acceptable) -  http://pir.georgetown.edu/pro/ 

NOTE: We the subcommittee, ask the CTDP to recommend a small set of DBs as prefered, or to give formal guidance on how users should navigate the proliferation of modification databases. 

### Rule 6
If all tags in a proteoform use the same Key, the sequence may be PREFIXED with a single tag defining the Key followed by a plus sign.
```
[RESID]+SE[12]QUE[42]NCE
```
Here the numbers in brackets are accession numbers in the resid database
```
[mass]+SE[12]QUE[42]NCE
```
Here the numbers in brackets are masses
```
[formula]+SE[CH(2)]QUE[H(2)O]NCE
```

### Rule 7
The tag describing the terminal modifications is separated with a dash to the left of the N-terminal amino acid, and the right of a C-terminal amino acid.
```
[mass:-17.027]-QUENCE-[Amidation]
```

## Definitions
* Descriptor: Member of the tag. Could be a key-value pair, or a keyless entry.
* Human Readable: A strong emphasis is placed on human readability for proteoform names. Proteoforms should be names in a manner that would allow general audience members to know exactly the sequence of amino acids and the positions of any modifications, described in as accurate detail as possible.
* Key: An optional element of a descriptor that specifies the descriptor type. It must be followed by a colon and a value.
* Machine Readable: Adherence to the conventions described above should facility the creation and utilization of generic parsers so that proteoforms could be exchanged between users using a computer interface.
* Modification: Includes the addition and subtraction of specific atoms, atom combinations and/or masses, at a specific residue in a proteoform
* Proteoform: A specific set of amino acids arranged in a particular order, which may be further modified (cotranslationally, posttranslationally or chemically) at designated locations.
* Tag: The specified way of writing a localized modification. Everything between ‘[‘ and ‘]’ (inclusive). A collection of descriptors. 
* Value: Contents of a descriptor, such as the mass, chemical composition, or modification name.

## Best Practices
The best practices emphasize human readability and clarity of modification identities for publishing sequences.
* In the pipe-separated list, the most descriptive element should go first to improve human readability.
* If the identity of a modification is known, it should be listed. This improves the clarity over listing only masses or accessions.
* Rule 6 should be used when there is only one element in the tag -- otherwise, human readability is compromised.
* Spacing before and after each descriptor is arbitrary, and should be appropriately added to improve readability.
* In the case of multiple key value pairs, UniMod interim names without key are recommended to come first for human readability.

## Examples
```
[Acetyl]-S[Phospho|mass:79.966331]GRGK[Acetyl|Unimod:1|mass:42.010565]QGGKARAKAKTRSSRAGLQFPVGRVHRLLRKGNYAERVGAGAPVYLAAVLEYLTAEILELAGNAARDNKKTRIIPRHLQLAIRNDEELNKLLGKVTIAQGGVLPNIQAVLLPKKT[Unimod:21]ESHHKAKGK
```
This is one way to write Histone H4 with several modifications. It is human-readable and conforms to the best practices.
Long version: The sequence describes histone H4 having its N-terminal acetylated (Unimod interim name Acetyl), Serine 1 phosphorylated (Unimod interim name Phospho and mass 79.966331), Lysine 5 acetylated (Unimod interim name Acetyl, Unimod ID 1 and mass 42.010565) and Threonine 96 phosphorylated (Unimod accession 21). 
```
[Unimod]+[mod: Acetyl]-S[mod: Phospho| mass:79.966331]GRGK[mod:Acetyl|1 |mass:42.010565]QGGKARAKAKTRSSRAGLQFPVGRVHRLLRKGNYAERVGAGAPVYLAAVLEYLTAEILELAGNAARDNKKTRIIPRHLQLAIRNDEELNKLLGKVTIAQGGVLPNIQAVLLPKKT[21]ESHHKAKGK
```
Although this is valid, the UniMod accessions end up looking like mass, and thus may be less clear to a human reader. This violates best practices rule 3, which discourages the use of prefix notation with more than one descriptor. 
```
[Unimod]+[1]-S[21]GRGK[1]QGGKARAKAKTRSSRAGLQFPVGRVHRLLRKGNYAERVGAGAPVYLAAVLEYLTAEILELAGNAARDNKKTRIIPRHLQLAIRNDEELNKLLGKVTIAQGGVLPNIQAVLLPKKT[21]ESHHKAKGK
```
This is a valid and compact way of specifying Unimod accessions in multiple locations in the sequence. 
```
[myristoleylation|Myristoleyl(PSI-MOD)|info:Acylation]-MTLFQLLREHWVHILVPAGFVFGCYLDRKDDEK[di-Methylation|Dimethyl(PSI-MOD)]LTAFRNK[p-adenosine|N6-(phospho-5'-adenosine)-L-lysine(RESID)|RESID:AA0227|PSI-MOD:00232|N6AMPLys(PSI-MOD)]SMLFQRELRPNEEVTWK
```
Extensive description of PTMs using descriptors and IDs from different databases. Less common PTMs can so be better recognized.
```
MTLFQLLREHWVHILVPAGFVFGCYLDRKDDEKLTA[mass:-37.995001|info:unknown modification]FRNKSMLFQRELRPNEEVTWK
```
Unknown modifications are best described by their mass shift and marked as unknown.

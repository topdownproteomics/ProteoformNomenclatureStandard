# Rules for Ambiguity

**NOTE:** This is a *DRAFT* proposal for ambiguity support in a future version of ProForma.

### Rule 8 - Multiple Sites
Tags can apply to multiple locations by using a #group notation.
```
PROT[Phospho|#eg]EOS[#eg]FORMS[#eg]
```
This is read as a named group 'eg' indicates that a Phosphorylation exists on either T4, S7, or S12.

### Rule 9 - Range
Tags can apply to a section of the amino acid backbone using a range notation.
```
PROT[mass:+19|A->]EOSFORMS[<-A]
```
This is read as a +19 Da mass shift exists somewhere from T4 to S12, inclusive.

### Rule 10 - Completely Unlocalized
Completely unlocalized tags can be applied at the beginning with a question mark.
```
[Phospho]?PROTEOSFORMS
```
This is read as a single Phosphorylation exists somewhere on this proteoform.

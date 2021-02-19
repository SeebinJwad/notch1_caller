# NOTCH1 Mutation Caller Algorithm
The mutation caller algorithm behind the notch1 mutation caller website.
## Dependencies
## Inputs
This algorithm reads inputs using HGVS Sequence Variant Nomenclature, so please read their documentation. Input structures for substitutions is provided as an example:
> Format: “prefix”“position_substituted”“reference_nucleotide””>”new_nucleotide”, e.g. g.123A>G
> “prefix” = reference sequence used = g.
> “position_substituted” = position nucleotide sustituted = 123
> “reference_nucleotide” = nucleotide at reference position = A
> ”>” = type of change is a substitution = >
> “new_nucleotide” = substituted nucleotide = G
## Batch Inputs
Currently, we do not have batch input capability. However, the program will loop following every output, making for a more efficient workflow.
### Here is the code snippet of potential splice mutation callbacks:
```python
    if '_splice' in check:
        if check[:check.find('_SPLICE')] != str(pos[0]) or len(
                check.replace(str(pos[0]), '', 1).replace('_SPLICE', '', 1)) != 0:
            return colored('INVALID INPUT: SPLICE MUTATION INCORRECTLY ENTERED', 'red')
        for a in range(1, len(c_exonb) - 1, 2):
            if pos[0] == c_exonb[a] / 3:
                return 'Valid input: Splice mutation detected'
        return colored('INVALID INPUT: AMINO ACID POSITION GIVEN DOES NOT MATCH THE END OF AN EXON BORDER', 'red')
    if len(pos) > 2 or len(pos) == 0:
        return colored('INVALID INPUT: AT LEAST ONE AMINO ACID POSITION MUST BE GIVEN BUT A MAXIMUM OF TWO IS ALLOWED',
                       'red')
    pos.extend([0] * (2 - len(pos)))```

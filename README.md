![Website](https://img.shields.io/website?down_color=green&down_message=online&up_color=green&up_message=online&url=http%3A%2F%2Fnotch1.tk%2F)
# NOTCH1 Mutation Caller Algorithm
The mutation caller algorithm behind the [NOTCH1 Mutation Caller Website](http://notch1.tk/).
## Dependencies
* [re](https://docs.python.org/3/library/re.html) - built-in module
* [termcolor](https://pypi.org/project/termcolor)
* [pandas](https://pypi.org/project/pandas)

*Note: Transitive dependencies are not listed*
## Inputs
This algorithm reads inputs using [HGVS Sequence Variant Nomenclature](https://varnomen.hgvs.org/), so please read their documentation. Input structures for substitutions is provided as an example:
> Format: “prefix”“position_substituted”“reference_nucleotide””>”new_nucleotide”, e.g. g.123A>G
## Batch Inputs
Currently, we do not have batch input capability. However, the program will loop following every output, making for a more efficient workflow.
### Outputs
Here is a table of all output sections:

Output Title | Output Values
------------ | -------------
Domain | [NOTCH1 Domain Knowledgebase](https://www.uniprot.org/uniprot/P46531#family_and_domains)
Impact on Function | Inactivating/Activating
Confidence Score | Low/High
Eligibility | Eligible/Ineligible

*Note: Only if the mutation's loss-of-function is inactivating (true) and the output is given a high confidence score will the patient be deemed eligible for the NOTCH1 trial.*

## NOTCH1 Domain Knowledgebase
Domains are listed in the [UNIPROT NOTCH1 Database](https://www.uniprot.org/uniprot/P46531#family_and_domains). However, we believe our domain/mutation spectrum is more accurate:

![NOTCH1 Domains](/imgs/notchdomains.jpg)

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
    pos.extend([0] * (2 - len(pos)))

# NOTCH1 Mutation Caller Algorithm
The mutation caller algorithm behind the notch1 mutation caller website.

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

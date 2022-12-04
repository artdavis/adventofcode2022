# Day 4: Camp Cleanup
https://adventofcode.com/2022/day/4

## Part 1

**In how many assignment pairs does one range fully contain the other?**


```python
#%qtconsole
```


```python
import numpy as np
from IPython.display import Markdown
```


```python
count = 0

with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    for line in fid:
        a, b = line.strip().split(',')
        a1, a2 = [int(x) for x in a.split('-')]
        b1, b2 = [int(x) for x in b.split('-')]
        avals = set(range(a1, a2 + 1))
        bvals = set(range(b1, b2 + 1))
        minlen = min(len(avals), len(bvals))
        overlap = avals & bvals
        if len(overlap) == minlen:
            # One range is fully contained
            #print(overlap)
            count += 1
        else:
            # Neither range is fully contained
            #print(False)
            pass
```


```python
#display(Markdown("One range is fully contained in the other **{}** times.".format(count)))
```

## Part Two

In **how many assignment pairs do the ranges overlap?**


```python
count2 = 0

with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    for line in fid:
        a, b = line.strip().split(',')
        a1, a2 = [int(x) for x in a.split('-')]
        b1, b2 = [int(x) for x in b.split('-')]
        avals = set(range(a1, a2 + 1))
        bvals = set(range(b1, b2 + 1))
        overlap = avals & bvals
        if len(overlap) > 0:
            # There's at least one overlap
            #print(overlap)
            count2 += 1
        else:
            # There is no overlap
            #print(False)
            pass
```


```python
#display(Markdown("There's at least one overlap **{}** times.".format(count2)))
```


```python

```

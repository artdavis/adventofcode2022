# Day 3: Rucksack Reorganization
https://adventofcode.com/2022/day/3

## Part 1

Find the item type that appears in both compartments of each rucksack.
**What is the sum of the priorities of those item types?**


```python
%qtconsole
```


```python
import numpy as np
from IPython.display import Markdown
```


```python
alphas = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
priorities = dict(zip(alphas, range(1, 53)))

# Priority sum
psum = 0
with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    for line in fid:
        stuff = line.strip()
        # Split stuff into compartments
        c1 = stuff[:len(stuff)//2]
        c2 = stuff[len(stuff)//2:]
        # Find shared items in both compartments
        shared = set(c1) & set(c2)
        # Priority value of shared item
        pval = priorities[shared.pop()]
        psum += pval
```


```python
#display(Markdown("The sum of priorities of the shared items is **{}**.".format(psum)))
```

## Part Two

Find the item type that corresponds to the badges of each three-Elf group.
**What is the sum of the priorities of those item types?**


```python
i = 0
elf = None
psum2 = 0
with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    for line in fid:
        if elf is None:
            elf = set(line.strip())
        else:
            elf &= set(line.strip())
        i += 1
        if 0 == i % 3:
            psum2 += priorities[elf.pop()]
            elf = None
```


```python
#display(Markdown("The sum of priorities of the shared items is **{}**.".format(psum2)))
```


```python

```

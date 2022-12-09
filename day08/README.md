# Day 8: Treetop Tree House
https://adventofcode.com/2022/day/8

## Part 1

Consider your map; **how many trees are visible from outside the grid?**


```python
#%qtconsole
```


```python
import numpy as np
from IPython.display import Markdown
```


```python
infile = 'input.txt'
#infile = 'testinput.txt'

dlist = list()
with open(infile, 'r') as fid:
    for line in fid:
        dlist.append([int(x) for x in line.strip()])

dat = np.array(dlist)
#dat

# Map of tree visibility. True if visible, False if not
vmap = np.zeros(dat.shape, dtype=bool)

def findvis(seq, vseq):
    # Find visibility per dequence of numbers
    for i, n in enumerate(seq):
        if 0 == i:
            vseq[i] = True
            ht = n
        elif n > ht:
            vseq[i] = True
            ht = n
        if n == 9:
            # No more trees can be visible
            break
            
#seq = dat[2]
#vseq = np.zeros(len(seq), dtype=bool)
#findvis(seq, vseq)
#vseq

for loop in range(4):
    for i, x in enumerate(dat):
        findvis(x, vmap[i])
    dat = np.rot90(dat)
    vmap = np.rot90(vmap)
```


```python
#display(Markdown("The number of visible trees is **{}**.".format(vmap.sum())))
```

## Part Two

Consider each tree on your map. **What is the highest scenic score possible for any tree?**


```python
dat2 = np.array(dlist)
# Index values of lower and right edges
imax, jmax = np.array(dat2.shape) - (1, 1)
# Scenic scores
rscore = np.zeros_like(dat2)
lscore = rscore.copy()
dscore = rscore.copy()
uscore = rscore.copy()
it = np.nditer(dat2, flags=['multi_index'])
for x in it:
    i, j = it.multi_index
    #print("{}:{}".format(x, it.multi_index))
    if 0==i or 0==j or imax==i or jmax==j:
        # Edge score is always zero
        continue
    # Look to the right
    for y in dat2[i, j+1:]:
        rscore[i, j] += 1
        delta = x - y
        if delta <= 0:
            break
    # Look to the left
    for y in dat2[i, j-1::-1]:
        lscore[i, j] += 1
        delta = x - y
        if delta <= 0:
            break
    # Look down
    for y in dat2[i+1:, j]:
        dscore[i, j] += 1
        delta = x - y
        if delta <= 0:
            break
    # Look up
    for y in dat2[i-1::-1, j]:
        uscore[i, j] += 1
        delta = x - y
        if delta <= 0:
            break
score = lscore * rscore * dscore * uscore
```


```python
#display(Markdown("The highest possible scenic score is **{}**.".format(score.max())))
```

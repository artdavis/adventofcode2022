# Day 1: Calorie Counting
https://adventofcode.com/2022/day/1

## Part 1

Find the Elf carrying the most Calories. **How many total Calories is that Elf carrying?**


```python
#%qtconsole
```


```python
import numpy as np
from IPython.display import Markdown
```


```python
tlist = list()
with open('input.txt', 'r') as fid:
    sublist = list()
    for line in fid:
        v = line.strip()
        if '' == v:
            tlist.append(np.array(sublist))
            sublist = list()
        else:
            sublist.append(int(v))
```


```python
sums = [x.sum() for x in tlist]
```


```python
#display(Markdown("The Elf carrying the most calories is carrying **{}** calories".format(np.max(sums))))
```

## Part Two

Find the top three Elves carrying the most Calories. **How many Calories are those Elves carrying in total?**


```python
paresums = sums.copy()
maxsums = list()
for _ in range(3):
    maxsums.append(np.max(paresums))
    paresums.remove(maxsums[-1])
```


```python
#display(Markdown("The top three Elf calories sum is **{}**.".format(np.sum(maxsums))))
```


```python

```

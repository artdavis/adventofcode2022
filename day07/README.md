# Day 7: No Space Left On Device
https://adventofcode.com/2022/day/7

## Part 1

Find all of the directories with a total size of at most 100000.
**What is the sum of the total sizes of those directories?**


```python
#%qtconsole
```


```python
#import numpy as np
import re
from IPython.display import Markdown
```


```python
# regex for matching on file size
r = re.compile('(\d+)\s')
```


```python
cwd = list()
sdict = dict()
with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    for line in fid:
        if line.startswith('$ cd'):
            # Changing directories
            _, _, d = line.strip().split()
            if d == '/':
                cwd = ['/']
            elif d == '..':
                cwd.pop()
            else:
                cwd.append(d)
            continue
        #print(cwd)
        m = r.match(line)
        if m:
            path = tuple(cwd)
            # Size of a file reported
            val = int(m.group(1))
            if path in sdict:
                sdict[path] += val
            else:
                sdict[path] = val
            # Add this value to every parent
            p1 = list(path)
            while p1:
                p1.pop()
                if p1:
                    p2 = tuple(p1)
                    if p2 in sdict:
                        sdict[p2] += val
                    else:
                        sdict[p2] = val
```


```python
dsum = 0
for k, v in sdict.items():
    if k != ('/',) and 100000 >= v:
        dsum += v
```


```python
#display(Markdown("The sum of the total sizes of those directories is **{}**.".format(dsum)))
```

## Part Two




```python
diskspace = 70000000
unused = diskspace - sdict[('/',)]
needed = 30000000
need_to_delete = needed - unused
#display("Still need to delete: {}".format(need_to_delete))
```


```python
sdict2 = {v: k for k, v in sdict.items()}
vsorted = sorted(sdict2.keys())
for v in vsorted:
    if need_to_delete <= v:
        dval = v
        break
```


```python
#display(Markdown("The size of the smallest directory to delete is **{}**.".format(dval)))
#display(Markdown("The directory is {}".format(sdict2[dval])))
```


```python

```

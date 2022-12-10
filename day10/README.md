# Day 10: Cathode-Ray Tube
https://adventofcode.com/2022/day/10

## Part 1

Find the signal strength during the 20th, 60th, 100th, 140th, 180th, and 220th cycles.
**What is the sum of these six signal strengths?**


```python
#%qtconsole
```


```python
#import numpy as np
from IPython.display import Markdown
```


```python
infile = 'input.txt'
#infile = 'testinput.txt'
#infile = 'testinput0.txt'

# Capture info fo the following cycles:
cycap = {20, 60, 100, 140, 180, 220}

x = 1
cytrack = dict()
siglog = list()
#linetrack = dict()
cyc = 1

linecount = 1
with open(infile, 'r') as fid:
    for line in fid:
        cmd = line.strip()
        if 'noop' == cmd:
            cyc += 1
            if cyc in cycap:
                cytrack[cyc] = x
                siglog.append(cyc * x)
                #linetrack[cyc] = linecount
        elif cmd.startswith('addx'):
            op, val = cmd.split()
            for i in range(2):
                cyc += 1
                if 1 == i:
                    x += int(val)
                if cyc in cycap:
                    cytrack[cyc] = x
                    siglog.append(cyc * x)
                    #linetrack[cyc] = linecount
        else:
            raise ValueError("Unknown cmd: {}".format(cmd))
        linecount += 1
            
#for k, v in cytrack.items():
#    print("Cyc:{}; X:{}".format(k, v))
```


```python
#display(Markdown("The sum of signal strengths is **{}**.".format(sum(siglog))))
```

## Part Two




```python

```

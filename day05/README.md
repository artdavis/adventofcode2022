# Day 5: Supply Stacks
https://adventofcode.com/2022/day/5

## Part 1

**After the rearrangement procedure completes, what crate ends up on top of each stack?**


```python
#%qtconsole
```


```python
#import numpy as np
from IPython.display import Markdown
```


```python
stacktxt = list()
cmdlist = list()
getcmds = False
with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    for line in fid:
        if line.strip() == '':
            # Ignore blank line
            continue
        if line.strip().startswith('1'):
            stacknums = [int(x) for x in line.strip().split()]
            getcmds = True
        elif getcmds:
            cmdlist.append(line.strip())
        else:
            # Gather stack information
            l = line.strip('\n')
            l = l.replace('[', '').replace('] ', '_').strip(']')
            # Zeros are empty spaces on the stack
            l = l.replace('    ', '0_').replace('   ', '0')
            stacktxt.append(l.split('_'))

#for r in stacktxt:
#    print(r)
#display(stacktxt)
```


```python
stacks = {x: list() for x in stacknums}
for r in stacktxt[::-1]:
    for i, val in enumerate(r):
        if '0' != val:
            stacks[i+1].append(val)
#stacks

# Run the command list
for cmd in cmdlist:
    _, n, _, s0, _, s1 = cmd.split()
    n = int(n)
    s0 = int(s0)
    s1 = int(s1)
    for i in range(n):
        stacks[s1].append(stacks[s0].pop())

topcrates = ''.join([stacks[i][-1] for i in stacknums])
#topcrates
```


```python
#display(Markdown("The top crates are **{}**.".format(topcrates)))
```

## Part Two

**After the rearrangement procedure completes, what crate ends up on top of each stack?**


```python
stacks2 = {x: list() for x in stacknums}

for r in stacktxt[::-1]:
    for i, val in enumerate(r):
        if '0' != val:
            stacks2[i+1].append(val)
#stacks2

# Run the command list for order preserving operations
for cmd in cmdlist:
    _, n, _, s0, _, s1 = cmd.split()
    n = int(n)
    s0 = int(s0)
    s1 = int(s1)
    # Move the ordered group over
    stacks2[s1].extend(stacks2[s0][-n:])
    for i in range(n):
        # Pop them off where they came from
        stacks2[s0].pop()

topcrates2 = ''.join([stacks2[i][-1] for i in stacknums])
#topcrates2
```


```python
#display(Markdown("The top crates are **{}**.".format(topcrates2)))
```


```python

```

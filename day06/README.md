# Day 6: Tuning Trouble
https://adventofcode.com/2022/day/6

## Part 1

**How many characters need to be processed before the first start-of-packet marker is detected?**


```python
#%qtconsole
```


```python
#import numpy as np
from IPython.display import Markdown
```


```python
with open('input.txt', 'r') as fid:
#with open('testinput.txt', 'r') as fid:
    txt = fid.read().strip()
#txt
```


```python
def get_start(nchars):
    """
    Get start character number for first unique nchars
    """
    for i in range(nchars-1, len(txt)):
        tset = set(txt[i-(nchars-1):i+1])
        if len(tset) > (nchars - 1):
            # Start of packet marker detected
            #print(i+1, tset)
            break
    # Start character        
    return i + 1

# Start of packet:
sop = get_start(4)
```


```python
#display(Markdown("Start of packet is at character number **{}**.".format(sop)))
```

## Part Two

**How many characters need to be processed before the first start-of-message marker is detected?**


```python
# Start of packet message
som = get_start(14)
```


```python
#display(Markdown("Start of message is at character number **{}**.".format(som)))
```


```python

```

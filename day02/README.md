# Day 2: Rock Paper Scissors
https://adventofcode.com/2022/day/2

## Part 1

**What would your total score be if everything goes exactly according to your strategy guide?**


```python
%qtconsole
```


```python
import numpy as np
from IPython.display import Markdown
```


```python
# A: Opponent rock
# B: Opponent paper
# C: Opponent scissors
# X: You rock
# Y: You paper
# Z: You scissors

# X (rock) beats C (scissors)
# Y (paper) beats A (rock)
# Z (scissors) beats B (paper)

windict = {'X': 'C',
           'Y': 'A',
           'Z': 'B'}
drawdict = {'X': 'A',
            'Y': 'B',
            'Z': 'C'}
valdict = {'X': 1, # Rock is 1 pt
           'Y': 2, # Paper is 2 pts
           'Z': 3, # Scissors is 3 pts
          }

def outcome(oppo, you):
    # Score for the round
    if windict[you] == oppo:
        # WIN!
        return 6 + valdict[you]
    if drawdict[you] == oppo:
        # TIE
        return 3 + valdict[you]
    else:
        # LOSE
        return 0 + valdict[you]
```


```python
score = 0
with open('input.txt', 'r') as fid:
    for line in fid:
        score += outcome(*line.strip().split())
```


```python
#display(Markdown("Your total score will be **{}**.".format(score)))
```

## Part Two

Following the Elf's instructions for the second column,
**what would your total score be if everything goes exactly according to your strategy guide?**


```python
# A: rock (+1)
# B: paper (+2)
# C: scissors (+3)

# X: You must lose
# Y: You must draw
# Z: You must win

# key: oppo, val: how you win
windict2 = {'A': 'B',
            'B': 'C',
            'C': 'A'}
# key: oppo, val: how you draw
drawdict2 = {'A': 'A',
             'B': 'B',
             'C': 'C'}
# key oppo, val: how you lose
losedict2 = {'A': 'C',
             'B': 'A',
             'C': 'B'}
valdict2 = {'A': 1, # Rock is 1 pt
            'B': 2, # Paper is 2 pts
            'C': 3, # Scissors is 3 pts
           }

def outcome2(oppo, you):
    # Score for the round
    if windict2[oppo] == you:
        # WIN!
        return 6 + valdict2[you]
    if drawdict2[oppo] == you:
        # TIE
        return 3 + valdict2[you]
    else:
        # LOSE
        return 0 + valdict2[you]

def playround(oppo, strat):
    if 'X' == strat:
        # Must lose
        return outcome2(oppo, losedict2[oppo])
    elif 'Y' == strat:
        # Must draw
        return outcome2(oppo, drawdict2[oppo])
    elif 'Z' == strat:
        # Must win
        return outcome2(oppo, windict2[oppo])
    else:
        raise ValueError("Unsupported strategy: {}".format(strat))
```


```python
score2 = 0
with open('input.txt', 'r') as fid:
    for line in fid:
        score2 += playround(*line.strip().split())
```


```python
#display(Markdown("Your total score will be **{}**.".format(score2)))
```


```python

```

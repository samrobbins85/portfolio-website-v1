+++
categories = ["coursework", "python"]
coders = []
date = 2019-01-21T00:00:00Z
description = "A range of code relating to Algorithms and Data Structures"
draft = true
github = ["https://github.com/samrobbins85/ADS-Coursework"]
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1593535123/Big-o-approx-logo_ci9nny.svg"
title = "Algorithms and Data Structures"
type = ""
[[tech]]
logo = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793276/logos/logos_python_pjlesq.svg"
name = "Python"
url = "https://www.python.org/"

+++
## Hash Table

The code for this algorithm can be found in `Question 1/q1.py`

This adds keys to a hash table of size 19 using the hash function defined by _h(k)=6k+3 mod 19_

In the first implementation `hash_quadratic` collisions are handled by probing

```python
def hash_quadratic(d):
    #initialize table
    table = ["-"]*19
    flag=0
    #consider each integer k in the input
    for k in d:
        flag=0
        #if k is already in the table this is a duplicate so move to next integer in the input
        #note this check for a duplicate is using the functionality of python rather than checking using a linear probe
        if k in table:
            continue
        #apply the hash function
        i = (6*k+3) % 19
        init=i
        #initialize count that checks whether linear probe has considered each bucket and is now full
        count = 0
        #while bucket is already filled
        while table[i] != "-":
            #move to next bucket
            i = (init+count*count) % 19
            #increment count
            count += 1
            #if table is full
            if count == 18:
                flag=1
                #can return table as nothing further can be added
                break
        if flag==1:
            continue

        #table[i] is empty so k can be added here
        table[i] = k
    #now each part of the input has been considered return the table
    return table
```

In the second implementation, `hash_double` collisions are handled using double hashing with the secondary hash function _h'(k)=11-(k mod 11)_

```python
def hash_double(d):
    #initialize table
    table = ["-"]*19
    flag=0
    #consider each integer k in the input
    for k in d:
        flag=0
        #if k is already in the table this is a duplicate so move to next integer in the input
        #note this check for a duplicate is using the functionality of python rather than checking using a linear probe
        if k in table:
            continue
        #apply the hash function
        i = (6*k+3) % 19
        init=i
        #initialize count that checks whether linear probe has considered each bucket and is now full
        count = 1
        #while bucket is already filled
        while table[i] != "-":
            #move to next bucket
            i = (init+count*(11-(k%11))) % 19
            #increment count
            count += 1
            #if table is full
            if count == 20:
                flag=1
                #can return table as nothing further can be added
                break

        if flag==1:
            continue
        #table[i] is empty so k can be added here
        table[i] = k
    #now each part of the input has been considered return the table
    return table
```

## Ephemeral numbers

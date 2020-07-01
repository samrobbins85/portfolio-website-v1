+++
categories = ["coursework", "python"]
coders = []
date = 2019-01-21T00:00:00Z
description = "A range of code relating to Algorithms and Data Structures"
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

This code calculates the number of ephemeral numbers between two values.

A positive integer is k-ephemeral if its k-descendent sequence ends in 1, otherwise it is k-eternal.

The k-descendant sequence of a positive integer begins with the integer and then each successive term is the k-child of the previous one. The sequence terminates if it reaches a 1 or a term is repeated.

The k-child of a positive integer is the number obtained by taking the kth power of each digit and adding them.

This is implemented using the following function

```python
def count_ephemeral(n1,n2,k):
    # Create a list of the powers required for the given value of k
    power_list=[x**k for x in range (10)]
    # Count keeps track of the number of ephemeral numbers
    count=0
    # Create two tables, one to store the eternal numbers, and one to store the ephemeral numbers
    eternal=set()
    eph=set()
    for n in range (n1,n2):
        # Current sequence stores all the values in the current sequence
        current_seq=set()
        # This checks if n has been seen before or if it is 1, in any of those cases it will break out of the loop
        while n not in current_seq and n not in eternal and n not in eph and n!=1:
            # Add the new number to the current sequence
            current_seq.add(n)
            # Calculate the k child of n
            k_child=0
            while n:
                digit = n % 10
                k_child+=power_list[digit]
                n //=10
            n=k_child
        # If n is an ephemeral number add it, and the rest of the sequence to the list of ephemeral numbers
        if n==1 or n in eph:
            eph.update(current_seq)
            count+=1
        # Otherwise add the sequence to the list of eternal numbers
        else:
            eternal.update(current_seq)
    return count
```

## Sum and product expression

A sum and product expression is a statement containing positive integers, brackets and the plus and times operators. A sum and product expression i said to be good is none of the brackets are redundant. This function decides whether a sum and product expression is good. It is implemented using stacks and queues, the code for defining how these work is left out for brevity.

```python
def good_expression(expression):
    # For completeness, remove all the spaces from the string just in case there are any
    expression=expression.replace(" ", "")
    # Initialise flags for if the statement is valid, if a close bracket was the last term and if the stack became empty on the last loop
    flag=0
    empty=False
    valid = True
    # Initialise a stack to store the operators
    data=Stack()

    for i in expression:
        count=0
        # The below if statement will trigger if a close bracket occurred on the last loop
        if flag==1 and empty==False:
            after = i
            before = b
            # If there isn't a multiplication on either of the sides of a pair of brackets, the statement is invalid
            if before!="*" and after!="*":
                valid=False
                break
        # If empty is True, then the first bracket of the pair was the first thing in the string, so there would need to be multiplication on the other side
        elif empty:
            after = i
            if after!="*":
                valid=False
        flag=0
        empty=0
        # If I is an operator or open bracket, just push it to the stack
        if i=="*" or i=="+" or i=="(":
            data.push(i)
        # But if i is a close bracket, more needs to be done
        if i==")":
            # Check if the stack is empty, as I will be popping from it, if it is empty, then there is an error
            if data.isEmpty()==True:
                valid=False
                break
            # Temporarily make valid false, for the purpose of checking the symbols in the bracket
            valid=False
            b=data.pop()
            while b!="(" and data.isEmpty()==False:
                # There needs to be an addition somewhere in the bracket, otherwise it is unnecessary
                if b=="+":
                    valid=True
                count+=1
                b = data.pop()
            # If there wasn't an addition, then break out of the loop ad the expression is bad
            if valid==False:
                break
            # If the bracket only had one symbol in it, it is unnecessary, and so the expression is bad
            if count==0:
                valid=False
                break
            # If the stack is empty, set the flag for the next element to check against
            if data.isEmpty()==True:
                empty=True
                flag=1
                continue
            b=data.top()
            flag=1
    # If the flag was set on the last element
    if flag==1:
        # If the symbol before the brackets isn't a multiply, then the statement is false
        if b!="*":
            valid=False

    return valid
```

## Hybrid Merge Sort

For this algorithm, instead of recursively calling Merge Sort until the list to be sorted has length 1, we will implement Selection Sort to sort any list of length 4 or less. This algorithm will output a sorted list from largest to smallest.

First I implemented a function to perform Selection Sort

```python
def SelectionSort(list):
    for i in range (0,len(list)):
        elem=list[i]
        pos=i
        for j in range(i+1,len(list)):
            if list[j]>=elem:
                elem=list[j]
                pos=j
        list[i], list[pos] = list[pos], list[i]
    return list
```

Then the function which performs Merge Sort and calls the Selection Sort function when appropriate

```python
def HybridSort(nlist):
    # If the length of the list is less than or equal to 4, then sort using selection sort
    if len(nlist)<=4:
        nlist=SelectionSort(nlist)
    # Otherwise sort using merge sort, unless the list is of length 1
    if len(nlist)>1 and len(nlist)>4:
        # Find the middle of the list
        mid = len(nlist)//2
        # Use this to create two lists
        lefthalf = nlist[:mid]
        righthalf = nlist[mid:]

        HybridSort(lefthalf)
        HybridSort(righthalf)

        # Merging
        i=j=k=0
        # While the lists are not exhausted
        while i < len(lefthalf) and j < len(righthalf):
            # If the left half first index is greater than right half, add it to the output list
            if lefthalf[i] >= righthalf[j]:
                nlist[k]=lefthalf[i]
                # Increment the value of i so that the element would not be added multiple times
                i=i+1
            else:
                # Other wise the right half first index is larger, so add that
                nlist[k]=righthalf[j]
                # And again increment the index
                j=j+1
            # Increment k to jump to the next index in nlist
            k=k+1
        # If the loop has broken out to here then one of the lists is empty
        # Loop adding all the remaining elements of the lefthalf list, if it is empty then just move on
        while i < len(lefthalf):
            nlist[k]=lefthalf[i]
            i=i+1
            k=k+1
        # Loop adding all the remaining elements of the righthalf list, again, if it is empty then just move on
        while j < len(righthalf):
            nlist[k]=righthalf[j]
            j=j+1
            k=k+1
```
### Python | intersection of multiple lists having duplicate elements

 When n lists are given, and we need to find the common elements in it, using the set intersection way in python is a good method.  
 But converting lists into sets removes any duplicate element that the list might contain and we loose track if there were more than one time occurrence of a common element overall. 
 for e.g
 
 >   Input:- List1 = [ [2,3,4,5,3],[1,2,3,6,7,3],[3,7,8,9,3,1,2] ]
 
 >       common output:- 2 3 3
 
 **1. If we try using the intersection method of sets:-**
 
 ```
 #code
 >>> d = [[2, 3, 4, 5, 3], [1, 2, 3, 6, 7, 3], [3, 7, 8, 9, 3, 1, 2]]
 >>> print(set(d[0]).intersection(*d[1:]))
```

>       Output :- {2,3}

The above code will return {2,3} . It essentially converts a list into set. The * argument allows for multiple parameters to the method intersection on the set object.
It takes all parameters from index 1 and above and returns the intersection of the first list with the rest. 

**2. Method for lists having duplicate elements:-**

*Here, we consider the smallest length list and count the occurence of it's elements in other lists.
 * We chose the minimum as any number not occurring in minimum length list cannot be an element of intersection .
 * From it's elements' frequency occurrence in other lists, for each element we select the minimum frequency of occurrence which is our answer to the common elements in all lists.

* We store our input as list of lists. We have n lists.
* We sort our list elements according to length. Thus the list with minimum length has index zero.
* We count the frequency of digits in each list using built-in counter  function from the class Collections.
* We then build a dictionary of the elements present in our minimum length list and store it's frequency of occurrence in all other list.
* We then iterate through this dictionary and find the minimum times every element in the minimum length list occurs in all other lists.



```
# code
from collections import Counter

input_list = [[2, 3, 4, 5, 3], [3, 7, 8, 9, 3, 1, 2], [1, 2, 3, 6, 7, 3]]
common_keysdict = dict()


input_list.sort(key=len)  # sorting our list of lists according to length


min_list = input_list[0]

# >> makes a counter object for each list (counts the frequency of each element in each list)

freq = list(map(Counter, input_list))
#freq= [Counter({3: 2, 2: 1, 4: 1, 5: 1}), Counter({3: 2, 1: 1, 2: 1, 6: 1, 7: 1}), Counter({3: 2, 7: 1, 8: 1, 9: 1, 1: 1, 2: 1})]

for ele in min_list:
    common_keysdict[ele] = []
    for counter in freq:
        if ele in counter:
            common_keysdict[ele].append(counter[ele])
        else:
            common_keysdict[ele].append(0)

# alternate dictionary comprehension for above code
alternate = {ele: [counter[ele] for counter in freq] for ele in min_list}

#common_keysdict={2: [1, 1, 1], 3: [2, 2, 2], 4: [1, 0, 0], 5: [1, 0, 0]}
# keys in common_dict:- elements of min_list  #values:-freq of occurrence in all lists from left to right

for key, value in common_keysdict.items():

    # taking minimum frequency of occurrence of the elements in min_set
    min_number_of_occurence = min(value)
    if min_number_of_occurence > 0:

        # printing the number as many times as common occurrence
        for x in range(min_number_of_occurence):
            print(key, end=" ")

print()
```

>   Output:-
>   2 3 3

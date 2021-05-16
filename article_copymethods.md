#### Python | copy lists and dictionaries

As we know python is a dynamically typed language, we do not need to declare a data type, it automically assigns the data type or data structure. So the major data types that we have are:- 
integer, float, string, list, dictionary , tuples, sets. The list , dictionary and sets are  mutable data types whreas the rest are immutable.

In the case of integer, float, string whenever a assignment of one variable to another happens , it automatically makes a new copy of the variable , in short assigns a new
memory location to that . e,g
  ```
  a = "hi, i am a string"
  b = a
  b = "I changed the string, my wish..."
  ```
This does not change the value of a it is still the one from previous operation. But if we do such kind of thing with lists:-

```
 list_a =[1,2,3,4]
 list_b =list_a
 list_b.append(5)
 
``` 
This will also append the value of 5 to a , which we do not want!This happens due to the mutable nature of lists and dictionaries, the assignments refer to the same address in memory.
So to get around this we use 

**1. The copy method**
```
list_b = list_a.copy()
```
**2. Using list splicing**
```
list_b= list_a[:]
```
**The deepcopy concept:**

Whenever we have nested lists , i.e lists inside lists, we use the deepcopy method
```
import copy

list_a =[[1,2,3],[3,4,5]]
list_b =copy.deepcopy(list_a)
```
This essentially copies recursively back to all the levels down and gurantees any operation on the
copy object will not affect the parent object. Deepcopy requires an external the copy module to be imported.

All these methods can also be used for python dictionaries.


  
  

# RASP

# Problem 1: Write an s-op that contains the indices in reverse order:

```
>> reverse_indices = length - indices - 1;
     s-op: reverse_indices
         Example: reverse_indices("hello") = [4, 3, 2, 1, 0] (ints)
>> 
.. reverse_indices("hello");
         =  [4, 3, 2, 1, 0] (ints)
```
# Problem 2: Write a function that "rotates" the input text by the specified number of characters:
```
>> def rotate(seq, shift) {
..       rotated_indices = (indices + shift) % length;
..       shifted_seq = aggregate(select(indices, rotated_indices, ==), seq);
..       return shifted_seq;
..   }
     console function: rotate(seq, shift)
```
Examples:
```
>> rotate(tokens, 0)("hello");
         =  [h, e, l, l, o] (strings)
>> 
.. rotate(tokens, 1)("hello");
         =  [e, l, l, o, h] (strings)
>> 
.. rotate(tokens, 2)("hello");
         =  [l, l, o, h, e] (strings)
```

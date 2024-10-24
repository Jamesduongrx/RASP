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

# Problem 3: Write a function that takes a sequence as input and "swaps every letter with its neighbor"
```

>> def swaptwo(seq) {
..       return aggregate(select(indices, indices + 1, ==), seq, "x") 
..              if indices % 2 == 0 
..              else aggregate(select(indices, indices - 1, ==), seq, "x");
..   }
>> 
.. def swap(seq) {
..       return aggregate(select(indices, indices, ==), seq, "x")
..              if length % 2 == 1
          and indices == length - 1
..              else swaptwo(seq);
..   }
>>
```
```

.. swap(tokens)("hello");
         =  [e, h, l, l, o] (strings)
>> 
.. swap(tokens)("ababab");
         =  [b, a, b, a, b, a] (strings)
```

# Problem 4: Write a function that returns the maximum value in the sequence repeated for every position

```
>> def maxseq(seq) {
..       sorted = sort(seq, seq);
..       lastone = length - 1;
..       return load_from_location(sorted, lastone);
..   }
     console function: maxseq(seq)
>> 
.. maxseq(tokens)("ababcabab"); #check
         =  [c]*9 (strings)
```

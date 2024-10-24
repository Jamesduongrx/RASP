# RASP

#Problem 1: Write an s-op that contains the indices in reverse order:

```
>> reverse_indices = length - indices - 1;
     s-op: reverse_indices
         Example: reverse_indices("hello") = [4, 3, 2, 1, 0] (ints)
>> 
.. reverse_indices("hello");
         =  [4, 3, 2, 1, 0] (ints)
```
#Problem 2: Write a function that "rotates" the input text by the specified number of characters:
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

#Problem 3: Write a function that takes a sequence as input and "swaps every letter with its neighbor"
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

#Problem 4: Write a function that returns the maximum value in the sequence repeated for every position

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
#Problem 5: Write a function that performs sequence reversal "autogeneratively"
```
>> dollar_pos = select_from_first(tokens, "$");
     selector: dollar_pos
         Example:

def reverse_ag(seq) {
..       dollar_loc = select_from_first(tokens, "$");
..       rest_string = aggregate(dollar_loc, indices);
..       return seq if indices <= rest_string else aggregate(select(indices, rest_string * 2 - indices, ==), seq, "");
..   }
     console function: reverse_ag(seq)
>>
```

```
.. reverse_ag(tokens)("hello$     ");

         =  [h, e, l, l, o, $, o, l, l, e, h] (strings)
>> .. reverse_ag(tokens)("hello$ ");
         =  [h, e, l, l, o, $, o] (strings)
>> 
.. reverse_ag(tokens)("hello$X");
         =  [h, e, l, l, o, $, o] (strings)
>> 
```
#Problem 6: Write a function that counts the number of times a certain token appears in the input sequence. 
```
.. def howmany(seq, token) {
..       return selector_width(select(seq == token, 1, ==))
          if contains(seq, token) else 0;
..   }
     console function: howmany(seq, token)
>> 
.. howmany(tokens, "a")("hello");
         =  [0]*5 (ints)
>> 
.. howmany(tokens, "h")("hello");
         =  [1]*5 (ints)
>> 
.. howmany(tokens, "l")("hello");
         =  [2]*5 (ints)
```

#Problem 7: Write a function that counts the number of times a certain token has appeared in the input sequence so far.
```
.. def howmany(seq, token) {
..       mask_ag = select(indices, indices, <=);
..       return round((indices + 1) * aggregate(mask_ag, indicator(seq == token)));
..   }
     console function: howmany(seq, token)
>> 
.. howmany(tokens, "a")("hello");
         =  [0]*5 (ints)
```

#Problem 8: Seeing if the token matches with character. 
```
def count_char(seq, char) {
..       return aggregate(full_s, indicator(tokens == char));
..   }
     console function: count_char(seq, char)

 count_char(tokens, "a");
     s-op: out
         Example: out("hello") = [0.0]*5 (floats)
```

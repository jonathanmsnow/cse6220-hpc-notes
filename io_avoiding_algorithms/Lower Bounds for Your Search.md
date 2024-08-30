![](Pasted%20image%2020240822193755.png)
# Solution
Intuition: Here since it is big O we are asking ourselves, what is the maximum number of bits we can learn given an L sized read. If we transfer L words of an array A where each element is a word. If each of these L words are indexed, we need to know to what power we need to raise 2 (since we are representing the indexes with binary) to index L words. This is equivalent to asking what is the Log L when using base 2.

So at most, we can "learn" at most log base 2 L bits which correspond to indices of A per an L-sized read. 

For further example, lets let L = 4.

Log L = Log 4 = 2

So this tells us, at most, we can learn 2 bits worth of indices. Does that makes sense?
Well, lets enumerate out all numbers we can represent with two bits:
1. 00 = 0
2. 10 = 1
3. 01 = 2
4. 11 = 3
So with two bits, we are able to index 4 of the entries of A. This makes sense as we have transferred L words which is equal to 4 entries in A since each entry is 1 word. So, it would make sense that we have "learned" enough bits to index these four entries.
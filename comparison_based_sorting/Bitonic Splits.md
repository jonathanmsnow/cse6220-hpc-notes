![](GT/Course%20Notes/CS%206220%20-%20HPC/Comparison-Based%20Sorting/images/bitonic-splits-sol.png)
# Solution
Recall what a bitonic split is:

When you pair the elements of a bitonic input sequence and then you apply mins and maxes to the pairs.
- This results in two bitonic subsequences
- To determine how to make these pairs, you can take n (your number of elements) and divide by 2. So for n = 32, you would pair together elements that are 16 elements apart from each other. That is to say, there are n/2 - 1 elements in between them.

We have the limit of using 1 comparator/column which makes sense because you can't have overlapping comparators which you would have given the pairing distance we calculate.

Let's also get an intuition for why we are using the plus comparator only in relation to the problem we are trying to solve. Recall that the "plus" comparator places the minimum of two values on the top output wire and the max on the bottom output wire. Applied across this network we will end up with all smaller values on the top half and the larger values on the bottom half.

As a final note, if we had to build out our own network, how could we determine the number of columns we need to get our result? Well, we see that the number of columns required is equal to the number of pairings that we need to make (i.e. n/2 = 4 columns).

To solve, we use that our input size n is 8. To determine the distance between pairs, we take n and divide by 2 and this gives us 4. We can select any starting point in the network to start a pair, then we just count n/2 elements from it to find its pair and mark it. To keep track of where we are, it's easiest to advance one from the start of the last pair, mark it and find the pair in the same way as before (i.e. count n/2 elements from the new start of the pair).

As noted in the lecture, this is only one solution, but we could select any starting point for pairs. We just need to make sure the spacing is the same, no pairs overlap in a column, and that no element of a pair is reused.
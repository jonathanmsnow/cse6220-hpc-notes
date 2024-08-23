![Alignment Exmaple Question](https://github.com/jonathanmsnow/cse6220-hpc-notes/blob/main/images/alignment-quiz-question.png?raw=true)
# Solution
At a high level we are asking: In transferring our n elements to do the reduction in fast memory, how many L sized transfers will be needed to move all of those elements. 

From here we know that we want the ratio of elements to L-sized transfers or $$n \over L$$.

This tells us it will take this many L sized transfers to move all n elements but that is assuming that each of our transfers are maximizing the the number of n elements in each L-sized transfer (I say maximizing here because in the case that L is 2 words for example and you need to transfer 3 elements,  even in best case your last transfer will have 1 element that is not actually an element of n). 
Keep the following in mind:
	1. When n > L: more than 1 transfer is required since all n inputs can't all fit inside one L sized transfer
	2. When n <= L: only one transfer is required because all n inputs can fit inside a single data transfer of size L\

Since our last transfer can potentially consist of items that are not one of our n elements (essentially when n does not evenly divide into L) we need to take the ceiling of our value (which the intuition here as to why we do this is we are working in a world where it isn't an option to do a partial L-sized transfer). So we now have 

$$ceil({n \over L})$$.

So, in our best case this is how many transfers we need. But if we are interested in the worst case, we need to consider the case where maybe our first read data transfer doesn't have values that are from of our n elements. This could happen if our data isn't aligned on an L-sized boundary. 

This would mean that at the worst case you are going to have to do 1 extra read that you wouldn't have had to do because you are loading in extra elements that are not from your n elements. This finally gives us our worst case 

$$ceil({n \over L}) + 1$$

![Proper Alignment Example](https://github.com/jonathanmsnow/cse6220-hpc-notes/blob/main/images/proper-alignment-example.png)\

Here we are aligned on an L word boundary so we can have an optimal set of reads where each data transfer of size L is maximizing the amount of elements it can transfer in each L-sized read.

![Improper Alignment Example](https://github.com/jonathanmsnow/cse6220-hpc-notes/blob/main/images/improper-alignment-example.png?raw=true)

Here the alignment is off so as we can see at both the beginning and the end we have sub-optimal reads where we are reading in data that is not one of the n elements we are interested in. This results in the extra 1 read we see in our final answer.

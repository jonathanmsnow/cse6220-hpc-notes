![](GT/Course%20Notes/CS%206220%20-%20HPC/Work-Span%20Model/images/reduction-tree.png)
# Solution
We are told that our number of Processors *P* is equal to n. Recalling the example for a reduction that is sequential we know that to load all n elements from A requires $$ceil({n \over P})$$
Given that *P* = n, all n elements can be loaded in parallel and since this is just a constant, we will ignore it for our analysis. 

Returning to the intuition we got from our previous sequential reduction example we know that each operation takes one unit of time.

Let's go down our list of options and consider them.
1. O(1) 
	 Intuitively, having the minimum time be a constant 1 does not make sense as we have dependencies between our vertices. This means that they cannot all be done at the same time which would allow us to do it in one time unit
2. O(log n) 
	 This is saying that at minimum, our time is going to be dependent on the number of levels in our reduction tree. This makes sense because taking log n (assuming log base 2 as we do) is essentially saying how many times can we half n until we get to one. We can see from our tree, at each level the number of operations is halving and at the root there is one final addition operation (the goal of 1 from our log n). The number of operations that it starts with is equal to our n elements that need to be loaded from A which is why we take log n. 
	 
	 We know at each level the number of operations will be less than n (at each level it approximately halves due to addition) and given that n = P, we can say for any given level L, the number of operations is on the level is less than or equal to P.
	 
	 This is important because that means at each level there are enough processors to process all operations on that level in parallel.
	 
	 What comes naturally from this is that if each level takes 1 unit of time to compute (due to all operations being in parallel), then the minimum amount of time it takes must be equal to the number of levels in our tree (for each level you must do 1 unit time of operations).
	 
	 This is what makes O(log n) our answer.
3. O(n) From our sequential reduction example, we know that this sort of run time occurs when for all n operations, they need to be done sequentially. If each one of our n operations takes 1 unit time and we can only process one computation at a time (due to dependencies of P = 1), that is when we will see it take n time
4. O(nlogn) We previously found that log n gives us the number of levels we have in our reduction tree and we considered this our running time because each level required one unit of time to process. Multiplying by n would imply that for each level, we would require n units of time to process our operations (worse than O(n) which was sequential!). This makes this not a possible answer given our assumption of n = P.
5. O(n^2) Again, this would be worse than our sequential reduction so this doesn't make sense knowing that at each level your number of operations is halving and that n = P.
![](GT/Course%20Notes/CS%206220%20-%20HPC/Work-Span%20Model/images/work-and-span-for-reduction.png)
# Solution
First its important to recall what the span is defined as. Span is the number of nodes along the longest path (critical path) of the DAG.

## Sequential Reduction
For our sequential reduction, we can first look at our DAG nodes that have no input dependencies (i.e. the loading of all n elements of A). From any of these nodes you can then go to an addition, but it should be noted that for any addition node after the first addition node has 2 input dependencies, the load and the dependency on the previous addition.

Since we are interested in the longest path for span, it follows naturally that we would find the longest path if we start from the very first addition. The number of nodes needed for adding all the elements is equal to n (since each load is an input dependency for an addition). Therefore, it follows that our Span is O(n).

## Tree Reduction
Again we start by looking at our initial loads of n elements since they don't have any input dependencies. From any one of these starting nodes our path will continue until it terminates at the point where there is one final addition. At this point we will have only one addition node. This suggests we have a problem where we are taking the logarithm.

We know that for each level in the tree, that each node points to a node in the next level (which means we couldn't have a path that goes along a single level). So that means at each level we can add at most one node to our count of our longest path. Therefore, the longest path must be determined by the number of levels we have which is the same as asking $$levels = log_2 n$$
This is because at each level we are take two nodes and this results in a single node (i.e. halving our n starting nodes at each level) until we get to a single node at the bottom. So, it follows that our longest path is equal to the number of levels so our final answer is $$O(log n)$$

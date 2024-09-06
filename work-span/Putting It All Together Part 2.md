![](GT/Course%20Notes/CS%206220%20-%20HPC/Work-Span%20Model/images/putting-it-all-together-2.png)
# Solution
First lets remember what this question is asking us. We want to know the span which is the path through the DAG that has the most vertices/nodes along it, which is the longest path through the DAG.

Thinking about our DAG and given our assumption that our parfor uses a divide and conquer approach we know from our first parfor, will add logn vertices to our path at most (because it divides our n elements to iterate on in half at each step which equivalent to log base 2 of n until it gets to 1). This intuitively makes sense because if you have logn levels at most, then the critical path will be at that upper limit.

At this point this gives us that our DAG would have D(n)=O(logn).

Since span is determined by the longest path through out DAG we already have a logn path. Then since at the end of this path we are going add on from loop 2 another logn we are essentially just doing an addition of those nodes to our path. Therefore we have $$D(n)=O(logn + logn)=O(logn)$$
Thinking of how nested loops work when calculating other metrics in big-O such as run time complexity, it might seem to make more sense that we would have logn * logn. The reason it is addition vs multiplication is we are interested in finding the length of one path through the DAG and in particular that path is the longest path. Let's take a simple example of n = 2 and look at what the DAG would look like.

![](GT/Course%20Notes/CS%206220%20-%20HPC/Work-Span%20Model/images/putting-it-all-together-2-dag.png)
So from our first par-for we add logn to our potential longest path (since log2 = 1). Now our longest path has grown by 1 (because the longest path could either by the left or right child of our root node). After our red line for our second par-for for each of the leaf nodes (prior to starting second par-for) of our original DAG, we add on log2 to our longest path. Of course there are vertices for our start and end which add to our actual span but these are constants so they are dropped. Additionally we technically have our middle portion growing by 2 * logn but for big-O that constant 2 is also dropped. So, here with this visual an intuitive feel for how the critical path grows and what dominates that growth can be seen.

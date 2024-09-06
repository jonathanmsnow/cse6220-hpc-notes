![](GT/Course%20Notes/CS%206220%20-%20HPC/Work-Span%20Model/images/work-and-span.png)

# Solution
Recall the definition of work and span:
1. Work W(n): The number of nodes in the directed acyclic graph (DAG)
2. Span D(n): The number of nodes along the longest path in a DAG

In this case, given that we have a grid, we can quickly calculate work by counting up the nodes along 2 sides and multiplying them together. Each side has 4 nodes so we have W = 4 * 4 = 16

Span is can be found just by looking for and counting the number of nodes along the longest path (from start to exit) which can be many different paths in this DAG. The value for span is S = 7.
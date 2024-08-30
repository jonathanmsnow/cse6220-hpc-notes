 ![](Pasted%20image%2020240827141949.png)
# Solution
We know that a binary search works by selecting an element in the middle of our collection and then slicing the collection in two and choosing what half to search in next depending on a comparison between our target value and our middle value. It continues this until the target element is found or there are no more elements left to search.

We know that 

We are looking for the worst case here since we are asked for the upper bound. For each part of the search we are going to need to load in the relevant elements. So, at each divide we will need to load in one of the halves based on our comparison to be processed in the next level of our search. If we are in the worst case where the element does not exist in the collection A, to determine that, we are going to need to compare our target value with the middle value of each slice we make. So, our transfers will be determined by how many times we can slice our original number of elements in half until only 1 element remains in our slice. That is equivalent to take the log base 2 of our number of transfers.

So, we know that we have n elements to start and that we need to move them in L-sized transfers giving us the usual $$n \over L$$ transfers. We know that it our actual number of transfers will be determined by how many times we will need to slice our collection in half so we take the log base 2 to get our final result $$O(log_2 {n \over L})$$ 
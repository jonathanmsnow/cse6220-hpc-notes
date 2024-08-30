![](Pasted%20image%2020240830152728.png)
# Solution
We want to get the total asymptotic cost for read transfers, then sorts, and then write transfers. First we should determine the cost of each of these for one iteration and build from there.

Additionally, the problem tells us to ignore f so we will leave that out (this makes sense because f is some constant between 0 and 1 and constants are dropped in big O).

## Reads
For a single read we are going to read in our chunk at i. We know that our chunks are all of size Z from our initial partitioning. So, this tells us for one read iteration, we need to transfer Z words of data and we know that we can handle an L-sized transfer. So how many transfers will this take? $${chunkSize \over transferSize} = {{Z} \over L}$$
We have to do this for all n/Z chunks so we have an upper bound on our total read transfers: $${n \over Z} * {Z \over L} = O({n \over L})$$
## Comparisons
We will take the same approach of looking at a single sort before looking at the total cost. We are told that we are using an optimal comparison sort which we know implies that it is runs in O(n* logn) time. 

In the case of looking at a single sort, we know each of our runs are of size Z so we let n = Z.

This means to make one sorted run our comparisons result in O(Z * logZ).

Now that we know what the upper bound is for a single sort of a run, we determine what the upper bound is across all runs (our total). We know from our loop that we have n/Z iterations to process all n/Z chunks. That means that we will be doing the sort operations n/Z times giving us our final complexity of $${n \over Z} * Z log_2 (Z) = O(n * log_2 Z)$$
## Writes
Once we know reads, it follows naturally that if we are going to write all of our data back to slow memory, we would need the same number of transfers, but to be sure we will follow the same steps.

First, we need to think about the size of a single run *i*. Given that sorting just rearranges the values within it, the size of it should be the same as when it was read which we know is of size Z. So in order to transfer a single run of size Z given our limit of L-sized transfers, we must can get our number of transfers as:
$${chunkSize \over transferSize} = {{Z} \over L}$$

Next, we ask again, how many chunks/runs do we have to do this for? Well our loop tells us that we have n/Z iterations (since each iteration i increments by 1). So we take our transfers required for a single write and multiply it by this number of iterations (the number of times we have to do it). Which again gives us:
$${n \over Z} * {Z \over L} = O({n \over L})$$

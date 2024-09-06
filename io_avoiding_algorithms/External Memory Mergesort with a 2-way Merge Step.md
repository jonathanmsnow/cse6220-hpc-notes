
![](Pasted%20image%2020240825132626.png)
# Solution
We are asked to get the comparisons and transfers of all runs using a 2-way merge. We should get the costs of Phase 1 and Phase 2 an then combine them.

## Phase 1
### Comparisons
We calculated the comparison costs for Phase 1 in [Partitioned Sorting Step Analysis](Partitioned%20Sorting%20Step%20Analysis.md).
We know that it has a cost of O(n log Z)


### Transfers
We also calculated the transfers in [Partitioned Sorting Step Analysis](Partitioned%20Sorting%20Step%20Analysis.md) and got our transfers as O(n/L)

## Phase 2

We know that pairs merged at each level k is 

$$ n \over 2^ks$$

This makes sense since 2^k s tells us the size of each run at k and we are just divide our n input elements across them to get number of pairs merged (# runs at level k).

We can calculate our number of levels by essentially asking ourselves how many times can we have our total number of runs until we have only one run (or in other words how can we combine all our runs in a two-way merge until there is only one run). This is directly related to taking the log base 2 of some number. So how many runs will we start with well that's: 

$$n \over s$$

Since we divide our n input elements into s-sized runs. So to get this number of runs down to by merging them pair wise we get 

$$log_2{n \over s}$$

### Comparisons
When merging together runs in a pair-wise fashion we are going to need to sort the items from the two runs into a new run. Since we are combining two runs together, the number of runs at each level halves at the next level and the number of items for each run then doubles (since two runs are being combined to one).

This generalizes so that we can say the number of items at some level k is 

$$2^k *s$$

Because our initial run has s items and at each level we go down, the number of items doubles. E.g. for 2 levels down from the first one (where each run is of size s) 

$$2s * 2s = 4s = 2^2s$$

In other words, since you have gone down two levels you have doubled your items in a run twice, which is equivalent to saying its 4 times more than it was.

So, this gives us the number of items per run at any level k given a size s.

If we zoom into a 2-way merge between two runs A and B, we know that A and B will have this many items in each of them

$$2^{k-1} * s$$

Why does that make sense? Well if we know at some level k we have 2^k * s items then one level before (i.e. k - 1) must use the expression above.

In order to compare all of these items and merge them into a single sorted new run, we will need to compare all the items of A with all the items of B. So this means we have a total number of comparisons of 

$$2^{k-1} s * 2^{k-1}s = 2 * 2^{k-1}s = 2^ks$$


Note: If it is not immediately clear, we just use that there is a like base ( 2 ) and since 2 = 2^1 that gives 2^k when multiplied with 2^k-1 (due to exponent rules)

So in order to compare all items in both runs and merge them into one we have $$2^ks$$
comparisons.

We are going to do this for all k levels for all pairs on that level so in total its number of levels * number of pairs per level * number of comparisons on that level

$$log_2{n \over s} *  {n \over 2^ks} * 2^ks = \theta(n * log_2 {n \over s})$$

For our tight bound on comparisons for phase 2.

### Transfers
We know that each run contains 2^(k-1)s items for some level k and a given size s so to determine the number of transfers for phase 2 we should break it down into what needs to get transferred. To merge two runs A and B we need to load them into fast memory from slow memory using L-sized data transfers. So in order to load A and B to produce the merged result of size 2^(k)s  we need 

$${2^{k-1}s \over L} + {2^{k-1}s \over L}$$

To write our result to create C we will need 

$${2^{k}s \over L}$$

transfers resulting in a total transfer cost of per pair A and B of 

$${2^{k-1}s \over L} + {2^{k-1}s \over L} + {2^{k}s \over L} = {1 \over L} (2^{k-1}s + 2^{k-1}s + 2^{k}s) = {1 \over L} (2*2^{k-1}s + 2^{k}s) = {1 \over L} (2^{k}s + 2^{k}s) = {2^{k+1}s \over L} $$

Now to generalize for the entirety of phase 2 we need to do this for all pairs at all levels giving us number of levels * number of pairs per level * number of transfers on that level

$$log_2{n \over s} *  {n \over 2^ks} * {2^{k+1}s \over L}  = 2{n\over L}log_2{n \over s}$$

# Combine Phase 1 and Phase 2
## Comparisons
Phase 1: $$n log Z$$
Phase 2:$$n * log_2 {n \over s}$$
Combined (note that because for our specific example we let the initial run size equal Z we let s = Z): 

$$n * log Z + n * log_2 {n \over Z} = n (log Z + log_2 {n \over Z}) = O(n * log_2 {n})$$

## Transfers
Phase 1: 

$$n \over L$$

Phase 2:

$$2{n\over L}log_2{n \over s}$$

Combined (subbing Z for s again and dropping constants for big O): 

$${n \over L} + 2{n\over L}log_2{n \over z} = {n \over L} (2log_2{n \over z} + 1) = O({n \over L} * log_2{n \over z})$$

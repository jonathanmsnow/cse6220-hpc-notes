[Lecture Video](https://edstem.org/us/courses/62694/lessons/114402/slides/631993)\
![](Screenshot%20from%202024-08-22%2017-50-58.png)

# Solution
Intuition: In our best case, we have that L <= n so we only need one transfer to load the entirety of our array A into fast memory (which of course means no other transfers necessary because there is no data beyond what is in A that needs to be searched).

With this in mind, let's think about the worst case. 

In the worst case, n > L (the number of items *n* is greater than the capacity of a single L-sized transfer), meaning we can't transfer all the values we need to search in one transfer. Therefore, we have a guaranteed first data transfer to begin our search which doesn't include all n items. Since a binary search slices our array n in half on each iteration, that means our n will be halving each time. Eventually n will reach a point where it is less than or equal to L. At this point, no further data transfers are required.

So we have one data transfer required to start and one final data transfer to load in that last block when n <= L. Let's remember that an assumption is that we can't do a partial data transfer (i.e. n/L cannot be fractional) so we must take the ceiling.

With this assumption our question is how many times do we have to divide our transfers required to transfer all n elements until n/L = 1 (all of our n elements fit inside one L-sized transfer). This is equivalent to asking ourselves what is the log base 2 of n/L.

So overall we have
$$Q(n;Z;L) = O(log_2{n\over L})$$

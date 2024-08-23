# Von Neumann Model
1. Processor: Performs basic compute operations
2. Fast memory: Fast but, small
	1. Use *z* which is size in words 
3. Slow memory: Large capacity, but slow

## Two Rules
1. Local Data Rule: Processor may only compute on data in fast memory
2. Block Transfer Rule: Slow-fast transfers in blocks of size *L* words
	1. For example: If we want to move *x* words from slow to fast memory, you need to pay to move L - x additional nearby words

### Costs
1. Work, W(n) = # of computation operations, for an input of size *n*
	1. Essentially, how many operations will the processor have to perform?
2. Data Transfers, Q(n; Z, L) = # of L-sized slow-fast transfers ("Loads and stores")
	1. The number of transfers is dependent upon the size of the cache and the block size. This will be referred to as 'Q' and can be called the I/O complexity

# Alignment
![[Pasted image 20240819172432.png]]
Here, we know that the array is of length N. In the worst case, our alignment is off. Lets look at a concrete example:
If our array size n = 4 and our word size L is 2, then it should take two transfers to load this data (i.e. Q = 2). This is in the case that the data is aligned, meaning our data (the array) is aligned on an L word boundary.
![[Pasted image 20240819173100.png]]

In the case that it is not, maybe our first read, gets one word before the first slot in our array and then uses one word for the first slot. Next it would read the middle 2 slots (2 words), finally it would read the last slot (word) and one word beyond that.
![[Pasted image 20240819173120.png]]

This is our worse case, so we know that Q < ceil(n/L) + 1. 

Z (The size of the cache) is not relevant here despite being part of the Q equation because you are touching each piece of data once, so the size of fast memory does not matter

# Algorithmic Design Goals
1. Work Optimality (We want low work)
	1. w(n) = theta(w*(n)) where * denotes the work of the best ram algorithm
2. High Computational Intensity (Operations per word) (We want high intensity)
	1. Maximize: I(n; Z, L) = w(n) /(L * Q(n; Z; L))

**Our goal is *low work* and *high intensity* **
## Intensity - Balance and Time
$$ \tau = time / word$$
$$ \alpha = time / op$$
$$ T_{comp} = \tau* W$$
$$ T_{mem} = \alpha * L * Q$$
$$ T \ge max(T_{comp}, T_{mem})$$
Which is equivalent to:
$$ Minimum Possible Execution = \tau * W * max(1, (\alpha / \tau)/(w/(L*Q)))$$$$\tau * W$$ Is the ideal computation time while
$$max(1, (\alpha / \tau)/(w/(L*Q))) = max(1, B / I)$$
is the communication (transfer) penalty and where $$B = \alpha / \tau$$
B is the Machine balance which is Ops per word
![[Pasted image 20240819152927.png]]

Normalized performance (our Rmax or maximum performance) is![[Pasted image 20240819151121.png]]

## Roofline Plots
![[Pasted image 20240819152204.png]]

We find that $$X_0 = B$$
We found this by thinking about the point at which Rmax becomes constant for any I. That gives us $$R_{max} = (W_* / W) / min(1, B/B) = (W_* / W) / min(1, 1) = (W_* / W)$$
This is because as I approaches infinity, the min of I / B or 1 will always be 1. This result also gives us $$y_0 = (W_*/W)$$


Takeaway:
1. Organize data access to increase reuse. Essentially, if you can avoid having to repeatedly load in the same block of data from slow memory to fast, you should.
2. Computational intensity and machine balance are directly related (in the communication/transfer penalty we see in performance)
3. Rule of thumb is that you want your intensity to at least match and ideally exceed your balance point. I think this makes sense because prior to this point your total Rmax will be reduced by some fraction due to how the penalty works in that algorithm. After intensity is greater than or equal to B (machine balance), the penalty is a constant value of 1 which given that it is multiplied against our work value, makes it so there is no penalty due to transfer
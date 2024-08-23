![Minimum Transfers Example](https://github.com/jonathanmsnow/cse6220-hpc-notes/blob/main/images/minimum-transfers.png?raw=true)
# Solution
When we are asking ourselves what is the "lower bound on the asymptotic number of transfers", we are essentially interested in the question of given the best case scenario how many transfers must we complete so that we can complete our computation (in this case sorting an array of n elements).

Well, intuitively, if we are going to sort all the n elements, we are going to need to load all n elements into our fast memory in order to process them (assuming there is nothing known about the array beforehand).

Given this, we are asking ourselves, how many L-sized transfers do I need to do to move all n elements? Well this is just a calculation of elements per L-sized transfer. Keep the following in mind:

	1. When n > L: more than 1 transfer is required since all n inputs can't all fit inside one L sized transfer
	2. When n <= L:, only one transfer is required because all n inputs can fit inside a single data transfer of size L

So, with this in mind we can say that a simple lower bound on the number of transfers is 

$$Q(n;Z,L) = \Omega(ceil({n \over L}))$$

Another option is 

$$Q(n;Z,L) = \Omega({n \over L})$$

This just ignores the need for a ceiling on the value which covers us in the case that n is not cleanly divided by L (resulting in a value that suggests partial transfers which doesn't necessarily make sense).

A tighter bound is given as 

$${n \over L} * {log({n \over L}) \over log({z \over L})}$$

This is beyond what is needed for understanding at this point though.

![Which is better example](https://github.com/jonathanmsnow/cse6220-hpc-notes/blob/main/images/which-is-better.png?raw=true)

# Solution
Our goals for a high performance algorithm are that:

1. It has low work i.e. minimizing W(n)
2. It has high intensity i.e. maximizing I

We see here that for work that algorithm 1 has less work due to it being solely based on n (our number of input elements) vs algorithm two with n log n (note that this is log base 2 since we are in a CS context). 

Based on our first goal, it seems like algorithm 1 is winning because 

$$W_1 < W_2$$

Now lets check how our second goal looks for this situation. While comparing the intensities we get that 

$$I_1 = {W_1 \over {L * Q_1}} = {n \over L * {n \over L}} = \theta(1)$$

Because the L cancel each other out as do the n resulting in it just being 1 (or constant time). For the second algorithm we have 

$$I_2 = {W_2 \over {L * Q_2}} = {n * log n \over L * {n \over L * log z}} = \theta(log n * log z)$$

Because our L values cancel each other then we divide n * log n by n / log z which is equivalent by multiplying by its inverse (log z / n) which cancels our the n factors and leaves us with our final result.

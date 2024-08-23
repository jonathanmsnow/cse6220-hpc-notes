![Intensity of Matrix Multiplication Part 2](https://github.com/jonathanmsnow/cse6220-hpc-notes/blob/main/images/intensity-of-matrix-multiply.png)
# Solution
Let's get to the root of what we are being asked. We want to know the tight bound of the intensity of this algorithm is. Well to know that we need to calculate what the intensity will be. Recall intensity is:

$$I(n; z, L) = {W(n) \over L * Q(n; Z, L)}$$

## Work Calculation
So taking this problem step by step, we first need to know the work completed W(n). 

Well we know that we are going to have to loop n times for each row *i* and for each row *i* we need to loop over each column *j* and for each row and column we need to iterate over all *k* elements in each row or column. Or in another way: 

$$r * c * e$$

Where r = # rows, c = # columns, and e = # elements for each row or columns (which # of elements in some row *i* and column *j* are equal given that we have n * n matrices allowing us to just call it e). 

What follows from having n x n matrices is that we have n rows per matrix, n columns per matrix, and n elements for each row or column, so then we have:

$$r * c * e = n * n * n = n^3$$

So our work $$W(n) = n^3$$

## Transfer Calculation
We are dividing our matrices into b x b sized blocks for reading and for each iteration of any of our loops our iterator is increasing by b. So in order to know the number of times we iterate, we would do the calculation 

$$n \over b$$

Where the intuition here for whywe do this is answering the question, how many b iterations can we do for a given n elements. We see from our algorithm that we iterate n/b times for the first loop and n/b times for our second loop before doing our first block read for C hat. Since we are reading a b * b block to get C hat and each element is a word, then we have a b^2 read there. So with one C hat read operation and our two loops which are nested we have: 

$$b^2 * {n \over b} *  {n \over b} = n ^2$$

A hat and B hat reads are nested in one more loop with n/b iterations so for each of those, we have 

$$b^2 * {n \over b} *  {n \over b} * {n \over b} = b^2 * ({n \over b})^3 = {n^3 \over b}$$

So all told we have a total number of reads

$$Q(n;Z;L) = n^2 + {n^3 \over b} + {n^3 \over b}$$

We will be looking at our intensity asymptotically, so we can drop the lesser terms and constants as the function is dominated by n^3 / b.

This gives us our final intensity of 

$$I(n; z, L) = {W(n) \over L * Q(n; Z, L)} = {n^3 \over 1 * {n^3 \over b}} = \Omega(b)$$

Now how do we get that the intensity can also be square root of z? Well we are given the assumption that our fast memory size z in words is

$$z =3b^2 + O(1)$$

Solving for b we get that:

$$b = \sqrt{{1\over3}(z - O(1))}$$

Looks scary... but let's put that value for b into our asymptotic notation so that we can drop constants. We get:

$$b = \sqrt{z}$$

So from this result we get:

$$I(n; z, L) = \Omega(b) = \Omega(\sqrt z)$$

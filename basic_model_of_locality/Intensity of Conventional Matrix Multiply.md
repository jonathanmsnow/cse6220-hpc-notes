![[Pasted image 20240823140240.png]]
# Solution
When being asked to find the tight bound on intensity, it is important to recall what intensity is defined as: 
$$I(n; z, L) = {W(n) \over L * Q(n; Z, L)}$$
In our case L = 1 so it can essentially be ignored in our calculations. 
## Work Calculation
First we will calculate W(n). 
1. Our first for loop will do the logic inside of it, n times. This first loop is keeping track of and iterating our *i* variable which is keeping track of what row we are looking at.
2. Our second loop also does the logic inside of it, n times. The variable *j* keeps track of what column we are processing. Since this is inside the outer loop which iterates n times and we are doing n iterations for this loop, we have n * n or n^2. Logically what we are doing so far is for each row *i* in A, we need to get some column *j* in matrix B.
3. Our final look iterates n times as well and keeps track of what element in either the row *i* or column *j* we are referencing. This is done *i* * *j* times giving us n * n * n = n^3
So therefore: $$
W(n) = n^3$$
## Transfers Calculation
Recall that Q(n;Z,L) is logically equivalent to # of L-sized slow-fast transfers ("Loads and stores"). So our question is then how many L-sized transfers must we do to get all of our elements for our calculation loaded into fast memory so we can do operations on them and then transfer our result back to our slow memory. Well we have three arrays of n x n size. That means that the total elements that need to be transferred is defined as $$n^2 + n^2 + n^2 = 3n^2$$
Because for each matrix (A, B, and C) they each have n^2 elements and at the most basic level we need to read or write n^2 elements for each when working with them. That's the idea we get intuitively when asking ourselves the amount of data that we are going to need to load in. 

The question now is based on our actual algorithm, what amount of transfers are needed.
1. read A[i, :], This read is in our first loop which iterates n times with *i* representing our row, this statement is shorthand for saying for row *i*, read all the elements in that row. We do this for all n rows and we know that each row is n elements long (from the fact that each matrix is n x n). This gives us n * n = n^2 data transfers for this line.
2. Read C[i, j], This is simply saying that for some row *i* and column *j* we are going to need to read the value for it at C into memory. Remember that given our loops for each row *i* we are going to iterate over all rows *j*. Given there are n rows and n columns we are going to have to do this operation n^2 times. The same principle applies to C[i,j] being stored.
3. Read B[:,j], This statement says for some column *j* read all the values in it. Again given that each matrix is n x n this means that in each column j there are n items. We have already established that our previous two loops with iterate over all columns and rows resulting in n^2 loads but this final piece will do a load of all n elements in column *j* resulting in a total data transfer cost for this line of n^3.

With each of our load or store lines covered we finally get that $$Q(n,L,Z) = 3n^2 + n^3$$
With our 3n^2 coming from accessing all the elements in A, B, and C (which also aligns with our intuitive sense of the minimum loads required to touch (read or store) all elements in each matrix) and n^3 coming from loading all *j* columns in B for every row in A.

Since n^3 dominates  the growth of this function and we are taking a tight bound we can drop the lesser 3n^2. So for intensity we have $$I(n; z, L) = {W(n) \over L * Q(n; Z, L)} = {n^3 \over 1 * n^3} = {n^3 \over n^3} = \Omega(1) $$

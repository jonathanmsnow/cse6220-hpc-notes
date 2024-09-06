
![](Pasted%20image%2020240826202733.png)
# Solution
When presented with this problem its best to break it down into parts but keep in mind a general model and intuition on how it will work. In this case we know that there will be some number of transfers needed at each level of the tree. Then this number of transfers will be done for every level. So we need to first know the per level transfers and then multiply that by the number of levels we have.

Let's first determine the cost to do 1 k-way were at some level i. It can be helpful to remember that a 2-way merge is actually just a specific case of a K-way merge. We know that for each level we are going to be merging K runs where K is less than Z/L (i.e. the number of runs we have will all fit into memory).

Additionally we know that each run has an initial size of about Z.

Zooming into a single level at i we know that the size of our new merged run will be $$k^is$$
because s represents the number of items per a run at the start of the merging. When all K runs are merged they will result in a new run with all K elements. As an example if K=3, at i = 1 we would have $$3^1s = 3s$$
At i - 1 we were at i = 0 or the start of our merge tree so it would make sense that the size of each run was just s. When we combine three s sized runs together, it should be a new run of size 3s. Essentially, at each level our number of items per a run grow by a factor of K (i.e. double, triple, quadruple, etc).

In order to do work on all of the items in our new run we will need to transfer them from slow memory (because after merging at the previous level the result is sent back to slow memory). This means we need to do our usual calculations of finding how many L-Sized transfers would be required giving us for one k-way merge run at level i 

$$k^is \over L$$

transfers per run to read all the items into fast memory.

Of course, we will also need to write our resulting merged run of size k^i*s back to slow memory which will require an additional 

$$k^is \over L$$

transfers. This leaves us with total transfers of

$${k^is \over L} + {k^is \over L} = 2 * {k^is \over L}$$

We can write this in big-O (and therefore drop the constant of 2) to get:


$$\theta({k^is \over L})$$

That is the transfers for one run, but we now need to consider how many runs there are at level i. We know that one run at level i has k^i * s items and that we start with n input items so its a question of dividing those n input items into those runs 

$$n \over k^is$$

So the total transfers for some level i is number of transfers for one run times the number of runs at that level 

$$2 * {k^is \over L} * {n \over k^is}=2 * {n \over L}$$

total transfers for one set of runs at level i. We will drop the constant 2 later when we write it in big-O.

Now, the questions is what is the total transfers for the whole merge process for the merge tree. With knowledge of the transfers required at one level we just need to multiply this by the number of levels we have. We are told that the number of levels is 

$$\theta(log_{Z \over L}{n \over L})$$

Which makes sense because we are essentially saying how many times will I need to divide my number of transfers required (n/L) by my fast memory split into L-sized chunks (Z/L) until n/L fits into my Z/L chunks (n/L <= Z/L).

So that means that in total we have 

$$O({n \over L} * log_{Z \over L}{n \over L})$$ 

total transfers for the entire merge.


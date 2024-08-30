![](Pasted%20image%2020240826200949.png)
# Solution
We are not fully utilizing the full size of the fast memory, Z. 

In the lower bound, we have  Z/L (which is the number of L-sized blocks in our fast memory of size Z) and n/L (the number times we can divide the input into L-sized data transfers). The lower bound takes our transfers and asks, "how many times can our required transfers (n/L) be put into our fast memory of Z in L-sized chunks". That is to say, how many transfers can we fit into our Z-sized memory. 2-way merging doesn't do better because we create 3 buffers of size L in fast memory of size Z. If 3L is not equal to Z then there is fast memory that is not being used increasing the number of transfers needed.
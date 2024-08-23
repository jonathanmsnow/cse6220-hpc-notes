![[Pasted image 20240823152920.png]]
# Solution
We first need to think about where is Machine Balance is used and what the question is really asking us. Well if we already had a machine that had some level of performance we know that performance and Machine Balance are related in the definition of performance: $$ R_{max} = {W_* \over W} * min(1, {I \over B})$$
We know from previous work that for efficient matrix multiplication that $$I = b = \sqrt z$$
Where b is the dimension of b x b blocks that we load into our fast memory. From this knowledge we have found a way to incorporate z into our performance equation by our knowledge of intensity.

Recall also that the right side of our performance equation is our penalty that we pay based on I and B. If we want to maintain that penalty at its current value regardless of I and B's values, we need to ensure that they remain proportional.

We are told that our machine balance B is doubled. In order to maintain this balance and keep our penalty consistent, we must also double our intensity. We are in control of our value of Z but need to keep in mind that the square root of it is being taken. If we want to double intensity we have $$
2I = \sqrt 4$$
We use 4 instead of 2 to account for our square root. So to maintain our current performance when machine balance double we need to increase the size of our Z word memory by a factor of 4.
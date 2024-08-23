![[Pasted image 20240819152204.png]]
# Solution
Notice that the axes of the roofline plot are the R_max(I) for the y axis and intensity for the x axis. R_max refers to our maximum performance and it is dependent on our intensity. Recall that R_max is defined as: $$
R_{max} = {W_* \over W} * min (1, {I \over B})$$
Where W_* is the best time in the pure RAM model and W is the work we perform for our algorithm.

B is our Machine balance ops/words (Machine dependent) defined as$$B = {\alpha \over \tau} = {{time \over word} \over {time \over operation}} = {operation \over word} $$

Now with all of this in mind, we see that at y_0 the graph become constant. Looking at our definition of R_max we know that the penalty part of the function either decreases our W_* / W by some decimal value or has no effect. The two cases are:
1. When I < B (i.e. I / B < 1), our R_max is penalized by the decimal of I / B
2. When I >= B (I / B >= 1), our R_max is not penalized because it is just being multiplied by 1 due to our min function taking the min(1, I/B)

So, it follows naturally that the point at which R_max becomes a constant value is when the penalty no longer applies (i.e. when I / B >= 1). We know that for any B, B / B = 1, so therefore at y_0 we must have that:
$$X_0 = B$$

This is because as I approaches infinity, the min of I / B or 1 will always be 1 and the first point at which I / B becomes 1 is when I = B.
Since R_max is a function dependent on the values of I, B, W, and W_star. When we set I = B we have:
$$R_{max} = {W_* \over W} * min(1, {I \over B}) = {W_* \over W} * min(1, {B \over B}) = {W_* \over W} * min(1, 1) = {W_* \over W}$$

Therefore at X_0 = B, we have that $$Y_0 = {W_* \over W}$$
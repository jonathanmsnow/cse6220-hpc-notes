![](GT/Course%20Notes/CS%206220%20-%20HPC/Work-Span%20Model/images/matrix-vector-multiply.png)
# Solution
First lets make sure we understand what loop 1 and loop 2 are doing and what this means in the context of a matrix vector multiply.

It seems that *i* is allowing us to iterate over the rows of A given how we are accessing A in the inner loop 2, so this is the responsibility of loop 1.

Loop 2 is iterating over the rows of A and each element of vector x using the iterator *j*.

Now, we know that inside of loop 2 we are accessing some element at i,j in A and an element in X at j and multiplying them. This result is then added to the resulting vector y at index i until all j elements have been iterated over.

We need to ask ourselves if this work can be done without a dependence (i.e. are each of these additions independent of each operations independent of each other). Well we see for an iteration j, we are updating the same index i in y. There is a dependence between each of our iterations in loop 2 because each iteration depends on the previous value written to y at index i to complete its calculation.

For loop 1, we can see that the use of i is consistent across the calculation and in the way that i is used there is no dependence because for some spawned subprocess using i:
1. The i value is used consistently in the spawned process to get and store the value in y at i
2. For i it is used to access just one row of i consistently.

For this reason, we can do loop one using a par-for.

To think about this more intuitively, we know for a matrix-vector multiply we take each row in some matrix A (we track this with i) and multiply each element j in this row by each element j in the vector x to get the resulting value in the output vector y. Each of the calculation to get the resulting value at i in y is independent of each other.

Contrast this with the calculations needed multiply the values and sum them in each row we see that these operations are dependent on each other so they cannot be done in parallel. We have a race condition because for some multiply being done at j we might access the value at i in y and after this another calculation at another j writes its result to i at y. Our first calculation finishes and then we would overwrite the value of the second calculation j resulting in a final result that is incorrect.
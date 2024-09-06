*Goal is to find the upper bound on processing time*
# Theorem
 $$T_P \le {W - D \over P} + D$$
 This theorem states that the upper bound on execution time is less than or equal to the time it takes to execute everything on the critical path D, plus everything off the critical path given P processors
# Derivation
## Part 1 (Setup)
Break execution into phases
	1. Each phase has 1 critical path vertex which implies there must be D(n) phases given that D(n) (span) is the number of vertices along the critical path. Each phase can be named after the number that the c.p. vertex is
	2. Non-critical path vertices in each phase are independent. In other words, each of the vertices can only have edges that either enter the phase or exit the phase. **They can never depend on one another.**
	3. Every vertex must appear in some phase. For some phase K there should W_k vertices and this rule implies that $$\sum_{k=1}^{D}W_k=W$$
	   Or in other words that the set of vertices in K should add up to the total number of vertices W (our measure of work)

Then to determine the time to execute phase K we have $$t_k=ceil({W_k \over P})$$
This implies that total execution time is equal to $$T_P = \sum_{k=1}^{D}t_k=\sum_{k=1}^{D}ceil({W_k \over P})$$

## Part 2 (Finish)
Break execution into D phases

We start with $$T_P\le\sum_{k=1}^{D}ceil({W_k \over P})$$
Then apply the identity $$ceil({a\over b}) = floor({a - 1 \over b}) + 1$$
To get $$T_P \le\sum_{k=1}^{D}floor({W_k - 1 \over P}) + 1$$
We know by definition that the floor of some value x is less than or equal to x. We are interested in the upper bound so we can take the greatest value that the floor can take on which is just the value itself. So we have: $$T_P\le\sum_{k=1}^{D}{W_k - 1 \over P} + 1 \le {W - D \over P} + D$$
Since if we sum all W_k we get W and subtracting or adding 1 D times is equivalent to just saying D (i.e. D * 1).



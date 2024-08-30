![](Pasted%20image%2020240825115247.png)
# Solution
First, we should determine what variable values we need to know and based on the algorithms listed we need:
1. n
2. L
3. Z
We already have been given n but this could have been calculated using the volume of data to sort equation and the fact that we know our record size r = 256 bytes $$n = 2^ {50} / r = 2 ^{50} / 2^ 8 = 2^{42}$$
We have to get this in tera ops so we can divide by 10^12 to get 4.40 when rounded to 3 significant figures.

Similarly lets calculate L and Z: $$L = 2^{15} / r = 2^{15}/2^8 = 2^7$$
$$Z = 2^{36} / 2^8 = 2^{28}$$
Going down the list we have then (remember each answer is divided by 10^12 to get it in tops):
b. $$2^{42} * log_2{2^{42} \over 2^7} = 2^{42} * log_2{2^{35}} = 2^{42} * 35 = 154 tops$$
d. $${2^{42} \over 2^7} * log_2{2^{42} \over 2^7} = {2^{35}} * log_2{2^{35}} = {2^{35}} * 35 = 1.2tops$$
e. $${2^{42} \over 2^7} * log_2{2^{42} \over 2^{28}} = {2^{35}} * log_2{2^{14}} = {2^{35}} * 14 = 0.481tops$$
f. $${2^{42} \over 2^7} * log_{2^{28} \over 2^{7}}{2^{42} \over 2^7} = {2^{35}} * log_{2^{21}}{2^{35}} = {2^{35}} * 1.67 = 0.0572tops$$


Insights:
Speedups can be seen with a reduction in tops as we go down the list. This is due in part to dividing moving your n sized data into L-sized transactions. By including z/L we are ensuring that we are using our fast memory of size z to the greatest extent possible given L.
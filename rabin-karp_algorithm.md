## Rabin-Karp algorithm {#rabin-karp-algorithm}

Rabin-Karp algorithm purposed hash function to identify pattern in given set of random number. We used Rabin-karp algorithm to solve string matching problem by **treated any character as number**.That’s would be easy, since all character have been mapped into**ascii standart**. For example, character ‘a’ is mapped to number 97, and ‘b’ mapped to 98\. To built a hash function, we should understand polynomial computation. Lets take a look this polynomial computation below:

formula

Hash of pattern “abc” in 26 character set is:

formula

We can say that p(abc) has highest order equal to two and hash value equal 68219\. So, if we try to find “_abc_” in the random set “_cgdabcef_”, we need to calculate possible hash value of each character in “_cgdabcef_” which matched to hash value of P(abc).

Lets take a look for an easy example:

Find pattern “abc” in set “cgdabcef”

Let:

**d** is how many atomic term

**n** is length of set “cgdabcef”

**m** is length of patten “abc”

**h** is highest order of pattern

**Hp** is hash value of pattern

**Hs****(****k****,** **m-****1****)** is hash value of set from index k to index m-1

Initialization:

d = 26

n = 8

m = 3

h = 262 = 676

Hp = P(abc) = 68219

Hs(k, m-1) = ?

Matching:

for 0 to m:

1.  Hs(0, m-1) = 69706

2.  Hs(1, m-1) = 72325

3.  Hs(2, m-1) = 70220

4.  Hs(3, m-1) = 68219

5.  Hs(4, m-1) = 68923

6.  Hs(5, m-1) = 69652

Result:

Found match in shift 3.

If we take a look for section matching in the example above, there look such heavy computation because we need to calculate hash value in each shift. We could optimize calculation of rehashing by implementing polynomial evaluation using **Horner’s Rule**:

formula

Suppose, we need to move from _p(i) =_ [_a__i_ _, a__k_]into _p(i+1) =_ [_ai__-1_ _, a__k+1_]:

formula

For example, we already know that p(cgd) is 69706\. Then to calculate next window, we need to calculate p(gda) that equal to **26 * (69706 – (97 * 26^2)) + 97** **= 72325**.

Another optimization is by using modulo to avoiding very long calculation. Since we know that that:

We can replace **(97 * 26^2)**from example before, into **(97 * 26^2)** **mod 97**. I used 97 here because intuitively we can say that any prime number is good to be **common divisor**.
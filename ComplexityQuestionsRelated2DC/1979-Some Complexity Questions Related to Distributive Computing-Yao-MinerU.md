# Some Complexity Questions Related to Distributive Computing*

(Preliminary Report)

Andrew Chi-Chih Yao

Stanford University and Xerox Parc

Palo Alto, California

# 1. INTRODUCTION.

Let  $M = \{0,1,2,\ldots,m-1\}$ ,  $N = \{0,1,2,\ldots,n-1\}$ , and  $f:M\times N\to \{0,1\}$  a Boolean-valued function. We will be interested in the following problem and its related questions. Let  $i\in M$ ,  $j\in N$  be integers known only to two persons  $P_{1}$  and  $P_{2}$ , respectively. For  $P_{1}$  and  $P_{2}$  to determine cooperatively the value  $f(i,j)$ , they send information to each other alternately, one bit at a time, according to some algorithm. The quantity of interest, which measures the information exchange necessary for computing  $f$ , is the minimum number of bits exchanged in any algorithm. For example, if  $f(i,j) = (i + j)mod 2$ , then 1 bit of information (conveying whether  $i$  is odd) sent from  $P_{1}$  to  $P_{2}$  will enable  $P_{2}$  to determine  $f(i,j)$ , and this is clearly the best possible.

The above problem is a variation of a model of Abelson [1] concerning information transfer in distributive computations. In Abelson's model, a "smooth" real-valued function  $f(x_{1}, x_{2}, \ldots, x_{s}; y_{1}, y_{2}, \ldots, y_{t})$  is to be computed with processor  $P_{1}$  knowing the values of  $x_{1}, x_{2}, \ldots, x_{s}$  and  $P_{2}$  knowing  $y_{1}, y_{2}, \ldots, y_{t}$ . Assuming that  $P_{1}$  and  $P_{2}$  can send values that are smooth functions to each other, Abelson obtained bounds on the minimum number of such values exchanged to compute  $f$ . Our model corresponds to a situation when  $f$  is a Boolean function, the  $x$ 's and  $y$ 's are Boolean variables ( $m = 2^{s}, n = 2^{t}$ ), and the values exchanged are bits. In contrast to the analytic flavor of Abelson's model, the present framework addresses computations which are combinatorial in nature.

# 2. THE DETERMINISTIC MODEL

Consider deterministic algorithms that control the bits exchanged between  $P_{1}$  and  $P_{2}$  in deciding the value of  $f$ . Initially the value  $i$  is known to  $P_{1}$ , and  $j$  to  $P_{2}$ . The computation proceeds in the following way:  $P_{1}$  first sends  $a_{1} \in \{0,1\}$  to  $P_{2}$ ; seeing  $a_{1}, P_{2}$  sends  $b_{1}$  to  $P_{1}$ ; seeing  $b_{1}, P_{1}$  sends  $a_{2}$  to  $P_{2}, \ldots$ . The choice of  $a_{k}$  (or  $b_{k}$ ) can depend on all the bits communicated so far. Precisely, an algorithm  $A$  specifies the Boolean functions  $\{h_{k}(i; u_{1}, u_{2}, \ldots, u_{k-1}), l_{k}(j; v_{1}, v_{2}, \ldots, v_{k}) \mid k = 1, 2, \ldots\}$  and the bits  $a_{k}, b_{k}$  are determined by  $a_{k} = h_{k}(i; b_{1}, b_{2}, \ldots, b_{k-1})$ .

$b_{k} = l_{k}(j;a_{1},a_{2},\ldots ,a_{k})$  . The computation ends when either  $P_{1}$  or  $P_{2}$  has enough information to determine  $f(i,j)$  , and sends a special symbol "halt" to the other processor. The cost  $\alpha (A)$  is defined to be the maximum number of bits (0 and 1) exchanged for any  $i\in M,j\in N$  The two-way complexity of  $f$  is defined as

$$
C (f; 1 \leftrightarrow 2) = \min  \{a (A) \mid A c o m p u t e s f \}.
$$

To study the quantity  $C$ , we first develop a more convenient way to view the computation. It will not be difficult to see that any algorithm as described above can be represented this way. We illustrate this with an example. Let  $f$  be the function defined in Figure 1, an algorithm  $A$  for computing  $f$  is given as a decision tree in Figure 2.

Each internal node in the decision tree has up to 4 children (two of them leaves and two internal nodes). Branches leading to leaves are labeled  $H$  (halt), and branches to internal nodes labeled  $X$  or  $Y$ . (We use  $X, Y$  instead of 0, 1 to avoid confusion with function values.) Moves are made by  $P_{1}$  and  $P_{2}$  alternately, starting at the root. Thus, label 1, 3, 5,... along a path are the signals sent by  $P_{1}$ , while label 2, 4, 6,... by  $P_{2}$ . The bit attached to a leaf gives the desired function value  $f(i, j)$ . We now describe the rules for selecting the branching at an internal node.

To each node  $v$  is associated a matrix  $S(v) \times T(v) \subseteq M \times N$ . At the root  $r$ , we have  $S(r) \times T(r) = M \times N$ . For an internal node  $v$  on an odd level (the root being on level 1) with children  $v_1, \ldots, v_l$  ( $l \leq 4$ ), we have  $T(v) = T(v_k)$  for  $1 \leq k \leq l$ , and  $\{S(v_k) \mid 1 \leq k \leq l\}$  form a disjoint partition of  $S(v)$ . On the even levels, similar conditions hold with the roles of  $S$  and  $T$  reversed. In  $P_1$ 's moves from a node  $v$  (on an odd level), it selects the unique child  $v_k$  with  $i \in S(v_k)$ . A similar statement can be said of  $P_2$ . A node  $v$  is a leaf if and only if  $f$  is constant in the block  $S(v) \times T(v)$ . Note that  $a(A) = \text{height}(A) - 1$ .

By induction on the value of  $mn$ , it can be shown that any algorithm can be represented in the above fashion. We shall now prove some results.

Definition. Let  $f$  be a Boolean-valued function on  $M \times N$ . We shall call a Cartesian product  $S \times T$  (where  $S \subseteq M$ ,  $T \subseteq N$ ) an  $f$ -monochromatic rectangle if  $f$  is constant over  $S \times T$ . A  $k$ -decomposition of  $f$  is a family  $\mathcal{F} = \{S_1 \times T_1, S_2 \times T_2, \ldots, S_k \times T_k\}$ .

![](images/98acd794b7a502a123ccf5fbcaa771d7ce6613330c02536919432aba62a451aa.jpg)



Figure 1 A function  $f$ , and the successive steps taken by the algorithm below in finding  $f(3,2)$ .


![](images/9cf585a2aa3df8ac0df3b51641f917d0bcc62ad300453df295966eb773fb5252.jpg)



Figure 2. An algorithm for computing  $f$ . The sequence of signals exchanged for input  $i = 3$ ,  $j = 2$  is XYH.


![](images/0e9e4ca220086565eb48d08a8e5408891ba4bb84f870e411416c5ce1817d69e5.jpg)



Figure 3 Illustration for  $C_{\varepsilon}^{\prime}(f;1 + 3 + 2)$  in Section 4.


of  $\mathbf{k}$  disjoint  $f$ -monochromatic rectangles that partition  $M \times N$ . Let  $d(f)$  be the minimum  $k$  such that a  $\mathbf{k}$ -decomposition of  $f$  exists.

Theorem 1.  $C(f;1\leftrightarrow 2)\geq \log_2d(f) - 2$

Corollary. Let  $\mathfrak{f}_n$  be the set of all Boolean-valued function on  $N \times N$ . Then, with probability  $1 - O(2^{-n^2 / 2})$ , a random  $f \in \mathfrak{g}_n$  satisfies

$$
C (f; 1 \mapsto 2) \geq \log_ {2} n - 4.
$$

Proof. Let  $A$  be an optimal algorithm for computing  $f$ , represented in the form of a tree as described earlier. As each internal node has at most two children that are leaves, it follows that

$$
\begin{array}{l} d (f) \leq \text {n u m b e r o f l e a v e s} \\ \leq 2 \times I (f), \tag {1} \\ \end{array}
$$

where  $I(f)$  is the number of internal nodes of  $f$ . As the internal nodes form a tree with height  $\alpha(A)$  and branching at most 2, we have

$$
\frac {(I (f) + 1)}{2} \leq 2 ^ {\sigma (A)}. \tag {2}
$$

From (1) and (2), we obtain

$$
2 ^ {\alpha (\Lambda)} \geq \frac {d (f)}{4}.
$$

This implies

$$
C (f; 1 \mapsto 2) \geq \log_ {2} d (f) - 2.
$$

This proves Theorem 1.

proof of Corollary. Since there are at most  $2^{2n}$  sets of the form  $S \times T$  with  $S \subseteq N$ ,  $T \subseteq N$  ( $S, T$  may be empty), the number of  $f \in \mathfrak{F}_n$  with  $d(f) \leq k$  is at most  $2^{2kn}$ . Now there are  $2^{n^2}$  distinct functions in  $\mathfrak{F}_n$ . The fraction of  $f$  satisfying  $d(f) > n/4$  (hence with  $C(f; 1 \leftrightarrow 2) > \log_2 n - 4$ ) is, therefore, at least

$$
\left(2 ^ {n ^ {2}} - 2 ^ {2 n n / 4}\right) / 2 ^ {n ^ {2}} = 1 - O \left(2 ^ {- n ^ {2} / 2}\right).
$$

This proves the corollary.

As  $C(f; 1 \leftrightarrow 2) \leq 2[\log_2 n]$  ( $P_1$  can simply send the binary representation of  $i$  to  $P_2$ ), the above corollary determines up to a factor of two the complexity of almost all Boolean-valued functions for large  $n$ .

Below we give some specific functions whose  $C(f; 1 \leftrightarrow 2)$  are of the order  $\log n$ , because of Theorem 1 (proofs omitted).

Example 1. The identification function:  $f(i,j) = \delta_{ij}$  for  $i,j \in \{0,1,\dots,n-1\}$ .

Example 2. The relatively-prime testing function:  $f(i,j) = 1$  iff  $i$  and  $j$  are relatively prime, where  $i,j \in \{0,1,\dots,n-1\}$ .

Example 3. The ordering function:  $f(i, j) = 1$  if  $0 \leq i \leq j < n$ .

Example 4. The set-intersection function:  $f(i, j) = 1$  iff the k-th bits of  $i$  and  $j$  are both 1 for some  $k$ , where  $i, j \in \{0, 1, \ldots, n - 1\}$ .

How good is the bound given in Theorem, as a function of  $\mathbf{k}$ ? The following theorem states that it can be achieved (up to a constant factor) if  $f$  has a "planar"  $d(f)$ -decomposition.

Definition. A k-decomposition of  $f, \mathfrak{f} = \{S_1 \times T_1, S_2 \times T_2, \ldots, S_k \times T_k\}$ , is planar if each  $S_i$  (and  $T_i$ ) consists of a block of consecutive integers.

Theorem 2. If  $f$  has a planar  $k$ -decomposition ( $k \geq 1$ ), then

$$
C (f; 1 \leftrightarrow 2) \leq \frac {2 \log_ {2} k}{\log_ {2} (4 / 3)} + 6.
$$

Proof. It is easy to see that  $C(f; 1 \leftrightarrow 2) \leq k$ . Therefore, the theorem is true for  $k \leq 4$ . We shall prove by induction that, for all  $k \geq 5$ ,

$$
C (f; 1 \leftrightarrow 2) \leq \frac {2 \log_ {2} (k - 4)}{\log_ {2} (4 / 3)} + 6. \tag {3}
$$

The inequality is clearly true for  $k = 5,6$ . Now suppose that  $k \geq 7$ . We shall show that, for some functions  $f_{1}$  and  $f_{2}$ , each with a planar  $(|3k / 4| + 1)$ -decomposition,

$$
C (f; 1 \leftrightarrow 2) \leq 2 + \max  \left\{C \left(f _ {a}; 1 \leftrightarrow 2\right) \mid a = 1, 2 \right\}. \tag {4}
$$

By the induction hypothesis, this would imply

$$
\begin{array}{l} C (f; 1 \leftrightarrow 2) \leq 2 + 2 (\log_ {2} ([ 3 k / 4 ] + 1 - 4)) / \log_ {2} (4 / 3) + 6 \\ \leq 2 \left(\log_ {2} (k - 4)\right) / \log_ {2} (4 / 3) + 6, \\ \end{array}
$$

hence completing the induction.

It remains to prove (4); we distinguish two cases.

Case A. There exists an  $s \in M$  such that there are  $h \geq \lceil k/2 \rceil$  distinct  $S_{i} \times T_{i}$  with  $i \in S_{i}$ . Without loss of generality, we can assume that they are  $S_{1} \times T_{1}, S_{2} \times T_{2}, \ldots, S_{h} \times T_{h}$ , and that  $T_{1}, T_{2}, \ldots, T_{h}$  are consecutive intervals covering the set  $N = \{0, 1, \ldots, n-1\}$ . Let  $N_{1} = T_{1} \cup T_{2} \cup \cdots \cup T_{\lceil h/2 \rceil}$  and  $N_{2} = N - N_{1}$ . It is easy to see that each  $M \times N_{i}$  ( $a = 1, 2$ ) intersects at most  $k - \lfloor h/2 \rfloor \leq (3k/4) + 1$  sets  $S_{i} \times T_{i}$  for  $j \in \{1, 2, \ldots, k\}$ . Thus each  $f_{a}$  ( $a = 1, 2$ ), the restriction of  $f$  to  $M \times N_{i}$ , has a planar  $(\lfloor 3k/4 \rfloor + 1)$ -decomposition. Since  $P_{2}$  can communicate to  $P_{1}$  in 1 bit whether the variable  $j$  (owned by  $P_{2}$ ) is in  $N_{1}$  or  $N_{2}$ , we obtain formula (4).

Case B. Suppose the condition in Case A is not satisfied. Let  $s \in S$  be the smallest  $s$  such that there are at least  $k/4$ $S_l \times T_l \subseteq M_1 \times N$ , where  $M_1 = \{0, 1, \ldots, s\}$ . Denote  $M - M_1$  by  $M_2$ . As each  $S_l$  is an interval, any  $S_l \times T_l$  that intersects  $M_1 \times N$  must satisfy either  $s \in S_l$  or  $S_l \times T_l \subseteq (M_1 - \{s\}) \times N$ . This implies that at most  $[k/2] + k/4 \leq 3k/4 + 1$  sets  $S_l \times T_l$  may intersect  $M_1 \times N$ . Thus, each  $M_a \times N$  intersects at most  $[3k/4] + 1$  sets  $S_l \times T_l$ , and hence each  $f_a$ , the restriction of  $f$  to  $M_a \times N$ , has a planar  $([3k/4] + 1)$ -decomposition. As only 1 bit sent from  $P_1$  to  $P_2$  suffices to express whether the variable  $i$  owned by  $P_1$  is in  $M_1$ , formula (4) follows.

This completes the proof of Theorem 2.

For general non-planar decompositions, we have the following theorem.

Theorem 3. There exists a constant  $\lambda >0$  such that, for all  $f$

$$
C (f; 1 \leftrightarrow 2) \leq \lambda \sqrt {d (f) \log_ {2} d (f)}.
$$

Skech of Proof. Let  $k = d(f)$ . We shall prove the theorem by induction on  $k$ . For each  $s \in M$ , let  $pat_s = \{l \mid s \in S_l\}$ . Either there exists an  $s$  with  $|pat_s| \geq 2\sqrt{k / \log_2 k}$  or there are altogether no more

than

$$
\left(\frac {k}{\lceil 2 \sqrt {k / \log_ {2} k} \rceil}\right) \leq e ^ {\lambda_ {1} \sqrt {k \log_ {2} k}}
$$

distinct  $pal_{\alpha}$ , where  $\lambda_1 > 0$  is a constant. In the former case, by an argument similar to the one used in the last theorem, one can show that there exit  $f_{\alpha} (a = 1,2)$  with  $d(f_{\alpha}) \leq k - \lfloor \sqrt{k / \log_2 k} \rfloor$  such that

$$
C (f; 1 \leftrightarrow 2) \leq 2 + \max  \left\{C \left(f _ {a}; 1 \leftrightarrow 2\right) \mid a = 1, 2 \right\}. \tag {5}
$$

In the latter case,  $O(\lambda_1 \sqrt{k \log_2 k})$  bits sent from  $P_1$  to  $P_2$  would enable  $P_2$  to decide the value of  $f$  immediately. The induction step can be carried out in either case.

We have proved Theorem 3.

# 3. THE PROBABILISTIC MODELS.

An interesting recent innovation in algorithm design is the inclusion of stochastic moves and the allowance for an  $c$  probability of error (See e.g. Rabin[2]). If each processor  $P_{i}$  is given a random number generator, can they determine the value of  $f$  with much less information exchanged? We discuss two models.

# 3.1 One-Way Probabilistic Communications.

To determine  $f(i, j)$ , processor  $P_{1}$  sends stochastically a string to  $P_{2}$ , based on which  $P_{2}$  stochastically decides the value of  $f(i, j)$  with chance of error  $\leq \epsilon$ . There are several different ways to define the complexity. In the simplest case, let all the strings transmitted be of uniform length. The 1-way probabilistic complexity of  $f$ ,  $C_{\epsilon}^{\prime}(f; 1 \leftrightarrow 2)$ , is then defined to be  $\lceil \log_2 k \rceil$ , where  $k$  is the minimum integer such that the following system of inequalities has a solution in  $\vec{p}_i = (p_{i1}, p_{i2}, \dots, p_{ik}), 1 \leq i \leq m$ , and  $\vec{q}_j = (q_{j1}, q_{j2}, \dots, q_{jk}), 1 \leq j \leq n$ .

$$
\left\{ \begin{array}{l l} \sum_ {i} p _ {i \ell} = 1 & \text {f o r a l l} i, j, \\ p _ {i \ell} \geq 0; \quad 1 \geq q _ {i \ell} \geq 0 & \text {f o r a l l} i, j, \ell , \\ \vec {p} _ {i}. \vec {q} _ {j} \geq 1 - \epsilon & \text {i f} f (i, j) = 1, \\ \vec {p} _ {i}. \vec {q} _ {j} <   \epsilon & \text {i f} f (i, j) = 0. \end{array} \right. \tag {6}
$$

Remark. Regard  $(f(i, j))$  as a 0-1 matrix, and denote by  $nrow(f)$ ,  $ncol(f)$  the numbers of distinct rows and columns of  $f$ , respectively. The 1-way complexity for the deterministic situation is easily seen to be  $\lceil \log_2(nrow(f)) \rceil$ .

The complexity for a special case, the identification function defined in Section 2, was studied in Rabin and Yao[3], and shown to be of order  $\log \log n$ . The following result determines  $C_{\epsilon}^{\prime}$  for a random  $f$ . However, the determination of  $C_{\epsilon}^{\prime}$  for specific functions in general seems very difficult.

Theorem 4. Let  $0 < \epsilon < 1/2$  be any fixed number. Denote by  $\mathfrak{F}_n$  the set of all Boolean-valued functions on  $N \times N$ . Then, with probability  $1 - O(2^{-n^2/2})$ , a random  $f \in \mathfrak{F}_n$  satisfies

$$
\left\lceil \log_ {2} n \right\rceil \geq C _ {\epsilon} ^ {\prime} (f; 1 \rightarrow 2) \geq \left\lceil \log_ {2} n \right\rceil - \log_ {2} \log_ {2} n - 2.
$$

Proof. The first inequality is clearly true for all  $f$ , so we need only prove the second inequality.

Let  $\mathfrak{F}_{n,k} \subseteq \mathfrak{F}_n$  denote the set of those  $f$ , for which k-component vectors  $\{\vec{p}_i, \vec{q}_j\}$  exist that satisfy (6). For each  $f \in \mathfrak{F}_n$  we choose a

solution and define a (2kn)-tuple

$$
\gamma (f) = \left(\lceil 4 p _ {i j} k / (1 - 2 c) \rceil , \quad \lceil 4 q _ {i j} k / (1 - 2 c) \rceil \mid 1 \leq i \leq n, 1 \leq j \leq k\right)
$$

Call  $\gamma (f)$  the representative of  $f$  Clearly, there are at most

$$
(1 + \lceil 4 k / (1 - 2 c) \rceil) ^ {2 k n} = \exp (2 k n \ln k + O (1))
$$

distinct representatives.

Now we assert that no two distinct  $f$  and  $f'$  in  $\mathfrak{T}_{n,k}$  may have the same representative. Otherwise, let  $\vec{p}_i, \vec{q}_j$  and  $\vec{p}_i', \vec{q}_j'$  be associated with  $f$  and  $f'$ , respectively. Choose  $s, t$  so that  $f(s, t) \neq f'(s, t)$ . According to (6), we have

$$
\left| \hat {p} _ {s}, \hat {q} _ {l} - \hat {p} _ {s} ^ {\prime}, \hat {q} _ {l} ^ {\prime} \right| \geq 1 - 2 \epsilon . \tag {7}
$$

On the other hand, as  $f$  and  $f'$  have the same representative, we have

$$
\begin{array}{l} \left| \hat {p} _ {n} \cdot \hat {q} _ {l} - \hat {p} _ {s} ^ {\prime} \cdot \hat {q} _ {l} ^ {\prime} \right| \leq \sum_ {\ell} p _ {o t} \left| q _ {t e} - q _ {t \ell} ^ {\prime} \right| + q _ {t c} \left| p _ {n e} - p _ {s e} ^ {\prime} \right| \\ \begin{array}{l} \leq 2 k \frac {1 - 2 \epsilon}{4 k} \\ <   1 - 2 \epsilon , \end{array} \\ \end{array}
$$

contradicting (7). This proves the assertion.

From the above discussions, we have

$$
\frac {| \mathfrak {F} _ {n , k} |}{| \mathfrak {F} _ {n} |} \leq \frac {\exp (2 k n \ln k + O (1))}{2 ^ {n ^ {2}}}.
$$

Take  $k = n / (4\ln n)$ . This leads to the conclusion that the probability is at most  $O(2^{-n^2 / 2})$ , for  $C_{\epsilon}'(f;1\to 2)\leq \lceil \log_2n\rceil -\log_2\ln n - 2$ . Theorem 4 follows easily.

# 3.2 Two-Way Probabilistic Communications.

In the basic 2-way model of Section 2, one can also allow stochastic moves in both processors. Let  $\epsilon$  (where  $0 < \epsilon < 1/2$ ) be the error probability allowed. Define  $\alpha'(A)$  to be the expected number of bits transferred for the worst input under algorithm  $A$ , and let  $C_{\epsilon}'(f; 1 \mapsto 2) = \inf \{\alpha'(A) \mid A \text{ an algorithm with error probability at most } \epsilon\}$ . The following result provides a limit to the power of stochastic algorithms. For example, it means that the 2-way probabilistic complexity for the identification function is also of order  $\log \log n$ .

Theorem 5. Let  $0 < \epsilon < 1/2$  be fixed. Then there exists a constant  $\lambda' > 0$  such that, for any  $f$ ,

$$
C _ {\iota} ^ {\prime} (f; 1 \leftrightarrow 2) \geq \lambda^ {\prime} \left(\log_ {2} \log_ {2} (n r o w (f)) + \log_ {2} \log_ {2} (n c o l (f)). \right.
$$

Proof. We omit the proof here because of its complexity.  $\blacksquare$

# 4. CONCLUDING REMARKS.

In this paper we have studied the information exchange needed, when two processors cooperate to compute Boolean-valued functions. The deterministic 1-way model is mathematically trivial and is completely understood. Below we shall comment on our understanding of the other three models and propose open questions.

A. The deterministic 2-way complexity. It is relatively well understood. Almost all functions in  $\mathfrak{F}_n$  have complexity  $\approx \log n$ , and

for many familiar functions, the complexity is determined up to a constant factor. One basic question remains unanswered, however. Let  $a_{k} = \max \{C(f;1\leftrightarrow 2)\mid d(f) = k\}$ . It is known that  $c\log k\leq a_k\leq c'\sqrt{k\log k}$ . What is  $a_{k}$ ?

B. The Probabilistic 1-way complexity. This is a most interesting subject for future research. It is known that almost all functions in  $\mathfrak{F}_n$  have complexity  $\approx \log n$ , yet no specific one is known to have this complexity. We conjecture that the ordering function (Section 2) has complexity  $\approx \log n$ .

C. The Probabilistic 2-way complexity. It is poorly understood, despite that there is a somewhat difficult lower bound result (Theorem 5). We do not even know the complexity of a random function in  $\mathfrak{F}_n$ . Note that Theorem 5 implies that the probabilistic 2-way communication improves over deterministic 1-way communication at most logarithmically.

D. More than two processors. Most of the results can be extended to communications between more than two processors in some form. We mention one situation that deserves special attention. Suppose three processors  $P_{1}, P_{2}, P_{3}$  cooperate to compute a function  $f(i, j)$ , with  $P_{1}$  knowing  $i$  and  $P_{2}$  knowing  $j$  initially. Instead of processors  $P_{1}, P_{2}$  communicating to each other, suppose that  $P_{1}, P_{2}$  both have an 1-way stochastic communication channel to processor  $P_{j}$  (see Figure 3), who then computes the value of  $f(i, j)$  with error probability less than  $\epsilon$ . Suppose that  $P_{3}$  uses a Boolean-valued function  $g$  on some domain  $M' \times N'$ , and computes  $f$  to be  $g(i', j')$  where  $i'$  and  $j'$  are the integers received from  $P_{1}$  and  $P_{2}$  respectively. The complexity  $C_{i}'(f; 1 \rightarrow 3 \leftarrow 2)$  is then the minimum of  $\log |M'| + \log |M'|$  over all possible choice of  $g, M', N'$ . An interesting alternative way to look at it is to regard  $C_{i}'(f; 1 \rightarrow 3 \leftarrow 2)$  as the log of the minimum table size  $|M'| |N'|$  needed, when we compute  $f(i, j)$  by "probabilistic hashing". What is the complexity of, say, the identification function?

E. NP-Completeness. Is the computing of the complexity  $C(f; 1 \mapsto 2)$  NP-complete?

# REFERENCES



[1] H. Abelson, Lower Bounds on Information Transfer in Distributed Computations, Proc. IEEE 19-th Annual Symp. on Foundations of Computer Science, Ann Arbor, 1978, pp. 151-158.





[2] M. O. Rabin, Probabilistic Algorithms, in Algorithms and Complexity: Recent Results and New Directions, edited by J. F. Traub, Academic Press, 1976, pp. 21-40.





[3] M. O. Rabin and A. C. Yao, in preparation.


# Probabilistic computations : toward a unified measure of complexity

Andrew Chi-Chih Yao

Computer Science Department

Stanford University

Stanford, California 94305

# 1. Introduction

The study of expected running time of algorithms is an interesting subject from both a theoretical and a practical point of view. Basically there exist two approaches to this study. In the first approach (we shall call it the distributional approach), some "natural" distribution is assumed for the input of a problem, and one looks for fast algorithms under this assumption (see Knuth [8]). For example, in sorting n numbers, it is usually assumed that all n! initial orderings of the numbers are equally likely. A common criticism of this approach is that distributions vary a great deal in real life situations; furthermore, very often the true distribution of the input is simply not known. An alternative approach which attempts to overcome this shortcoming by allowing stochastic moves in the computation has recently been proposed. This is the randomized approach made popular by Rabin [10] (also see Gill[5], Solovay and Strassen [13]), although the concept was familiar to statisticians (for example, see Luce and Raiffa [9]). Note that by allowing stochastic moves in an algorithm, the input is effectively being randomized. We shall refer to such an algorithm as a randomized algorithm.

These two approaches lead naturally to two different definitions of intrinsic complexity of a problem, which we term the distributional complexity and the randomized complexity, respectively. (Precise definitions and examples will be given in Sections 2 and 3.) To solidify the ideas, we look at familiar combinatorial problems that can be modeled by decision trees. In particular, we consider (a) the testing of an arbitrary graph property from an adjacency matrix (Section 2), and (b) partial order problems on  $n$

numbers, including sorting, selection, etc. (Section 3). We will show that for these two classes of problems, the two complexity measures always agree by virtue of a famous theorem, the Minimax Theorem of Von Neumann [14].

The connection between the two approaches lends itself to applications. With two different views (and in a sense complementary to each other) on the complexity of a problem, it is frequently easier to derive upper and lower bounds. For example, using adjacency matrix representation for a graph, it can be shown that no randomized algorithm can determine the existence of a perfect matching in less than  $O(n^{2})$  probes. Such lower bounds to the randomized approach were lacking previously. As another example of application, we can prove that for the partial order problems in (b), assuming uniform distribution (i.e., all n! permutations equally likely) always yields the greatest complexity.

We will also consider algorithms that allow errors (cf. Karp [6], Rabin[10]). Again useful connections (though not equality in this case) can be drawn between the distributional and the randomized complexities. For example, the  $O(n^{2})$  lower bound for perfect matching mentioned above still holds, even if we allow a randomized algorithm to make errors, say, 5 percent of the time.

Since discussions of low-order computational complexity have to be based upon precise models of algorithms, we shall treat (a) and (b) type problems separately in Sections 2 and 3. Directions for further research are discussed in Section 4.

# 2. Testing Graph Properties

# 2.1 Notations and Definitions

Let  $g_{n}$  be the set of all undirected graphs on  $n$  vertices. Assume that  $P$  is a graph property on  $g_{n}$ , that is, a mapping from  $g_{n}$  into {true, false}. Given any graph  $G$  in  $g_{n}$  represented by its adjacency matrix, we are interested in testing whether or not  $G$  has property  $P$  by successively probing entries of its adjacency matrix. In the standard model (see Rivest and Vuillemin [12]), an algorithm  $A$  for testing property  $P$  is represented as a binary decision tree, where branches correspond to whether a matrix entry tested is 0 or 1. To distinguish such conventional algorithms from the randomized algorithms to be described later, we call  $A$  a pure algorithm. For an input graph  $G$  of algorithm  $A$ , we use  $r(A, G)$  to denote the number of tests made by  $A$ . Let  $A$  be the family of pure algorithms that make no redundant tests. We are now ready to discuss the complexity concept in the distributional approach. Given a probability distribution  $d$  on  $g_{n}$ , the average cost of a pure algorithm  $A$  is defined by

$$
C (A, d) = \sum_ {G \in \mathbf {g} _ {n}} d (G) \cdot r (A, G).
$$

Under the input distribution  $d$ , the best that any pure algorithm can achieve is clearly min  $C(A, d)$ . We now define the distributional complexity for testing  $P$  to be

$$
F _ {1} (P) = \sup  _ {d} \quad \min  _ {A \in A} C (A, d).
$$

This quantity  $\mathbf{F}_1(\mathbf{P})$  captures the following complexity notion:

Provided that the distribution of inputs is known,  $\mathbf{F}_1(\mathbf{P})$  is the average cost we can always guarantee by finding a good algorithm..

We shall now explore the complexity concept from the randomized approach. A randomized algorithm R is specified by a probability distribution q on  $\mathcal{A}$ . We shall interpret R as an algorithm that has probability q(A) to proceed exactly as A. The expected cost of R for an input graph G is

$$
\mathrm {E} (\mathrm {R}, \mathrm {G}) = \sum_ {\mathrm {A}} \mathrm {q} (\mathrm {A}) \cdot \mathrm {r} (\mathrm {A}, \mathrm {G}).
$$

The intrinsic cost of R is defined to be  $\mathbf{E}(\mathbf{R},\mathbf{G})$  for the "worst" graph G, i.e., max E(R,G). A natural complexity measure of the problem from this viewpoint is thus the intrinsic cost of the best randomized

algorithm. That is, we define the randomized complexity for testing  $\mathbb{P}$  to be

$$
F _ {2} (P) = \inf  _ {R} \max  _ {G \in \mathcal {g} _ {n}} E (R, G).
$$

The quantity  $\mathbb{F}_2(\mathbb{P})$  tells us how much time the best randomized algorithm takes for testing  $\mathbb{P}$ .

A newly developed concept is to consider algorithms that allow a certain percentage of error in the final answer (see Karp [6], Rabin[10]). We shall now define the corresponding complexity measures for these classes of algorithms. Let us extend the family of pure algorithms  $A$  to a larger family  $A_{\mathfrak{o}}$ , consisting of all decision trees that give a "yes" or "no" answer for any input graph  $G \in \mathcal{G}_{\mathfrak{n}}$  (the answer need not be correct). For a decision tree  $A \in A_{\mathfrak{o}}$ , and an input  $G \in \mathcal{G}_{\mathfrak{n}}$ , let  $\epsilon(A, G) = 0$  if  $A$  gives the correct answer for  $G$ , and  $\epsilon(A, G) = 1$  otherwise. As before, let  $r(A, G)$  be the number of tests made by  $A$  for input  $G$ .

Let  $\pmb{\lambda}$  be a number between 0 and 1. For any input distribution  $d$ , let  $\beta (\lambda)$  be the subset of  $\mathbf{A}_0$  that consists of decision trees with error probability not exceeding  $\pmb{\lambda}$  under  $d$ . That is,

$$
\mathcal {B} (\lambda) = \left\{A \mid A \in \mathcal {A} _ {0}, \sum_ {G \in \mathcal {g} _ {n}} d (G) \in (A, G) \leq \lambda \right\}.
$$

The distributional complexity with error  $\lambda$  is defined as

$$
F _ {1, \lambda} (P) = \sup  _ {d} \quad \min  _ {A \in B (\lambda)} C (A, d)
$$

where  $C(A,d)$  is as given previously.

We now consider the complexity with error from the randomized approach. A distribution q on the family  $\lambda_{\circ}$  is said to be  $\lambda$ -tolerant if

$$
\sup  _ {G \in \mathbf {g} _ {n}} \sum_ {A \in \mathcal {A} _ {\circ}} q (A) \cdot \epsilon (A, G) \leq \lambda .
$$

To insure that the error probability is bounded by  $\lambda$  for all input, we can only allow randomized algorithms whose characterizing distributions  $q$  are  $\lambda$ -tolerant. For a randomized algorithm  $R$  characterized by a  $\lambda$ -tolerant distribution  $q$ , the expected cost for input  $G$  is

$$
\mathrm {E} (\mathrm {R}, \mathrm {G}) = \sum_ {\mathrm {A} \in \mathrm {A} _ {\mathrm {O}}} \mathrm {q} (\mathrm {A}) \mathrm {r} (\mathrm {A}, \mathrm {G}).
$$

The randomized complexity with error  $\lambda$  is then

$$
F _ {2, \lambda} (P) = \inf  _ {R} \max  _ {G \in \mathcal {g} _ {n}} E (R, G)
$$

where the infimum is taken over all randomized algorithms R with a  $\lambda$ -tolerant distribution. For  $\lambda = 0$ ,  $F_{1,\lambda}$  and  $F_{2,\lambda}$  are reduced to  $F_{1}$  and  $F_{2}$ , respectively.

# 2.2 Fundamental Theorems

The definitions of  $\mathbb{F}_1(\mathbb{P})$  and  $\mathbb{F}_2(\mathbb{P})$  naturally suggest methods for finding lower bounds to  $\mathbb{F}_1(\mathbb{P})$ , and upper bounds to  $\mathbb{F}_2(\mathbb{P})$ . In the first case, choose a specific distribution  $d$ , and a lower bound  $b$  for  $\mathbb{F}_1(\mathbb{P})$  can be obtained by showing that no pure algorithm can make less than  $b$  tests on the average under  $d$ . Similarly, upper bounds for  $\mathbb{F}_2(\mathbb{P})$  can be derived by analyzing the performance of specific randomized algorithms. These bounds may not be easy to obtain in practice, but at least we know what to attack. On the other hand, how can we prove lower bounds for  $\mathbb{F}_2(\mathbb{P})$  to know the limitation of the randomized approach? The following theorem thus is a useful bridge.

Theorem 1  $\mathsf{F}_1(\mathsf{P}) = \mathsf{F}_2(\mathsf{P}).$

Theorem 1 can be proved by using the famous Minimax Theorem of Von Neumann [14]. It is aesthetically nice as the two complexity views are actually the same. It also provides practical means for proving lower bounds to  $\mathbb{F}_2(\mathbb{P})$  and upper bounds to  $\mathbb{F}_1(\mathbb{P})$ . For example, limitations to the power of the randomized approach can now be established by considering "hard" input distributions. The following theorem suggests that distributions that have equal weights on isomorphic graphs in  $g_n$  are good candidates.

Theorem 2 Let  $d$  be any distribution on  $g_n$ . Then there exists a distribution  $d_0$  such that

(i) min C(A,d) 1 min C(A,d), and A∈A

(ii)  $d_{\circ}(G_1) = d_{\circ}(G_2)$  if  $G_1$  and  $G_2$  are isomorphic.

The exact evaluation of  $\mathbf{F}_{\mathbf{i}}(\mathbf{P})$  can be shown to be a linear programming problem. For small  $n$ ,  $\mathbf{F}_{\mathbf{i}}(\mathbf{P})$  can be effectively computed, and Theorem 2 can be used to the advantage of reducing the number of variables considerably.

For algorithms with error tolerance, the following theorem links the complexities developed from the two approaches.

Theorem 3  $\mathbf{F}_{2,\lambda}(\mathbb{P})\geq \frac{1}{2}\mathbf{F}_{1,2\lambda}(\mathbb{P})$  for  $0\leq \lambda \leq \frac{1}{2}$

# 2.3 Concrete Lower Bounds

In this subsection, we derive certain specific lower bounds for testing graph properties. By Theorems 1 and 3, it suffices to prove bounds only for  $\mathbf{F}_{1,\lambda}$ . Occasionally, we find it possible to derive stronger results for  $\mathbf{F}_{2,\lambda}$  directly.

Definition We call P a normal graph property on  $\mathcal{G}_{\mathrm{n}}$  if P(empty graph) = false. For any graph S in  $\mathcal{G}_{\mathrm{n}}$ , the size of S, denoted by  $\|S\|$ , is the number of edges in S. For a normal property P, a graph S is a minimal graph for P, if S is a smallest-sized graph satisfying  $P(S) = \text{true}$ . For any G in  $\mathcal{G}_{\mathrm{n}}$ , let  $\pi(G)$  denote the group of automorphisms for G. (An automorphism for G is a relabelling of the vertex set  $\{1,2,\ldots,n\}$  that leaves G invariant.)

Theorem 4 Let  $\mathbf{P}$  be a normal graph property on  $\mathcal{G}_{\mathfrak{n}}$ , S a minimal graph for  $\mathbf{P}$ , and  $0 \leq \lambda \leq 1/2$ . Let  $s = \| S \|$ . Then

$$
\mathrm {F} _ {\mathbf {i}, \lambda} (\mathrm {P}) \geq \left(\frac {1}{2} - \lambda\right) \frac {1}{\mathrm {s}} \binom {\mathrm {n}} {2} \quad \text {f o r} \mathrm {i} = 1, 2.
$$

The spirit of Theorem 4 is similar to a result of Kirkpatrick [7, Theorem 2.3]. To give an application, let  $\mathbf{P}$  be the property for a graph to be non-planar, then  $S$  is  $K_{3,3}$ , a 3 by 3 complete bipartite graph. Theorem 4 tells us that  $\Omega(n^{2})$  tests are required for any randomized algorithm, even allowing a 25% error. For more properties with a small minimal graph, see Kirkpatrick [7].

Theorem 4 can be generalized to bipartite graph properties. As in the worst-case complexity [7], this can then be used in conjunction with an embedding process to prove  $\Omega(n^2)$  lower bounds for various "connectedness" properties. The following theorems can be proved by a non-trivial embedding process.

Theorem 5 Let  $T$  be any tree in  $g_{n}$ , and  $P$  the property for a graph to contain  $T$  as a subtree. Then

$$
F _ {i, \lambda} (P) \geq \text {c o n s t a n t} \cdot n ^ {2} \quad \text {f o r} 0 \leq \lambda \leq 0. 1, i = 1, 2.
$$

Theorem 6 Let  $0 < k \leq n$ , and  $P$  the property of containing a clique of size  $k$ . Then

$$
F _ {i, \lambda} (P) \geq \text {c o n s t a n t} \cdot n ^ {2} \text {f o r} 0 \leq \lambda \leq 0. 1, i = 1, 2.
$$

Any graph property  $\mathbb{P}$  has a linear lower bound  $\mathbb{F}_{\mathbf{i}}(\mathbb{P}) \geq \Omega(n)$ . This can be seen as follows. Without loss of generality, we can assume  $\mathbb{P}$  to be normal. Let  $S$  be a minimal graph for  $\mathbb{P}$  of size  $s$ . It is easy to show that  $\mathbb{F}_{\mathbf{i}}(\mathbb{P}) \geq s$ . When we combine this with Theorem 4, we have

$$
F _ {i} (P) \geq \frac {1}{4} \max  \left\{s, \frac {n ^ {2}}{s} \right\},
$$

which implies that  $F_{i}(P) \geq \Omega(n)$ . From the viewpoint of showing bounds stronger than  $\Omega(n)$ , properties with  $s \approx \text{constant} \times n$  are the hardest to handle. The next theorem is often useful in such cases.

Theorem 7 Let  $S$  be a minimal graph for a normal graph property  $P$  on  $n$  vertices. Let  $\| S \| = s$ , then

$$
\mathrm {F} _ {\mathbf {i}} ^ {(\mathrm {P})} \geq \frac {\mathrm {s}}{\mathrm {s} + 1} \left(\frac {\mathrm {n} ! \mathrm {s} !}{\left| \mathcal {M} (\mathrm {S}) \right|}\right) ^ {1 / \mathrm {s}}, \quad \text {f o r} \mathrm {i} = 1, 2.
$$

As an illustration of its application, consider the property for a graph to be Hamiltonian. Clearly S is now a Hamiltonian circuit, and the group  $\pi(S)$  is the cyclic group on  $\{1,2,\ldots,n\}$ . Thus,  $s = n$  and  $|\pi(S)| = n$ . Therefore, for the Hamiltonian property P, we have

$$
\mathrm {F} _ {\mathbf {i}} (\mathrm {P}) \geq \frac {\mathrm {n}}{\mathrm {n} + 1} \left(\frac {\mathrm {n} ! \mathrm {n} !}{\mathrm {n}}\right) ^ {1 / \mathrm {n}} \approx \frac {\mathrm {n} ^ {2}}{\mathrm {e} ^ {2}} \quad \text {f o r i = 1 , 2 .}
$$

Similar results can be derived for the property of containing a perfect matching. Although we have not succeeded in extending Theorem 7 to lower bounds for  $\mathbf{F}_{\mathbf{i},\lambda}$  (with  $\lambda \neq 0$ ), for the special cases of being Hamiltonian and containing a perfect matching, the proofs can be modified to show the following theorem.

Theorem 8 Let  $\mathbf{P}_1$  and  $\mathbf{P}_2$  be the properties of being Hamiltonian, and containing a perfect matching, respectively, on  $g_n$ . Then, for  $\lambda \in [0,0.1]$ , we have

$$
F _ {2, \lambda} (P _ {i}) \geq \text {c o n s t a n t} \times n ^ {2} \quad \text {f o r} i = 1, 2.
$$

# 3. Partial Order Problems

The complexity concept discussed in Section 2 can be extended to any problem with a finite set of possible inputs and algorithms. Theorem 1 and Theorem 3 remain valid, and Theorem 2 also has an analogue if there is a "symmetry" in the problem. (We shall see an example below.)

Perhaps the most extensively studied decision tree problems are those connected with partial orders (e.g. [8]). We shall concentrate on a special class that involve element selections. (See Fredman [4], for example, for other types of partial order problems.) Let the rank  $\ell_{\mathrm{V}}(\mathbf{x})$  of an element  $\mathbf{x}$  in a linearly ordered set  $V$  be the number of elements less than or equal to  $\mathbf{x}$ . For positive integers  $n$  and  $k$  with  $n \geq k$ , let  $\mathbf{I}_{n,k} = \{(i_1, i_2, \ldots, i_k) | \text{the } i_j's \text{ are distinct integers between } l \text{ and } n\}$  be the set of all ordered  $k$ -tuples of distinct integers not exceeding  $n$ . A selection problem  $J$  on a set  $V$  of  $n$  elements is specified by a set  $J \subseteq I_{n,k}$ , and can be described as follows: Given a set  $V$  of  $n$  elements, we wish to find, by pairwise comparisons between the elements,  $k$  elements  $(x_1, x_2, \ldots, x_k)$  such that  $(\ell_{\mathrm{V}}(x_1), \ell_{\mathrm{V}}(x_2), \ldots, \ell_{\mathrm{V}}(x_k))$  is in  $J$ . For example, the sorting problem corresponds to the choice  $J = \{(1, 2, \ldots, n)\}$ ; and in the selection of the  $k$  smallest elements, we set  $J$  to be the set of all permutations of  $(1, 2, \ldots, k)$ .

For a selection problem  $J$  on a set  $V = \{x_1, x_2, \ldots, x_n\}$ , an algorithm  $A$  is a decision tree where each internal node performs a comparison of the form "  $x_i : x_j$ ". At each leaf of the tree, an output  $(x_{il}, x_{i2}, \ldots, x_{ik})$  is specified. Let us use  $F_i(J)$  and  $F_{i,\lambda}(J)$  to denote the complexity of the selection problem  $J$  as was done in Section 2. Theorem  $l$  is still true, so we have  $F_l(J) = F_2(J)$ . There are two interesting results on the complexity of selection problems that we shall now discuss.

Firstly, there is a nice symmetry for any selection problem. Intuitively, if we take any algorithm A, and relabel the elements of V in any way, A will be transformed accordingly into another valid algorithm. This observation can be used to derive the following result parallel to Theorem 2. Let us still use  $\mathfrak{A}$  for the set of algorithms, and  $C(A,d)$  for the average number of comparisons made by algorithm A under input distribution d.

Theorem 9 Let  $J$  be a selection problem on a set  $V$ , and  $d_u$  be the uniform distribution on the input, i.e., every linear ordering on  $V$  is equally likely. Then

$$
\min  _ {A \in \mathcal {N}} C (A, d _ {u}) = F _ {i} (J) \quad f o r i = 1, 2.
$$

Informally, Theorem 9 tells us that the uniform distribution is the "hardest" distribution, and we can find bounds to  $F_{i}(J)$  by studying optimal algorithms under  $d_{u}$ . There are many studies concerning the quantity  $\min_{A} C(A, d_{u})$  for various problems [2,8,11,15].

Some of these results involve rather difficult proofs. These results now acquire a new significance through Theorem 9. For example, it was shown by Floyd and Rivest [2] that for the problem of finding the median of  $n$  numbers,  $1.375n \leq \min_{A \in \mathcal{A}} C(A, d_u) \leq 1.5n$ .

In the new interpretation, we can state that, (1) for an arbitrary distribution  $d$ , there always exists a (pure) algorithm that makes less than 1.5 n comparisons on the average; and (2) any randomized algorithm must make at least an expected 1.375 n comparisons for some input.

Now, for the second point of interest. So far in our models we have not seen any randomized algorithm that is order-of-magnitude better than the worst-case complexity of conventional (pure) algorithms solving the same problem. We shall now demonstrate the superiority (in the order-of-magnitude sense) of a randomized algorithm allowing a small error in a selection problem. Such an example comes from the selection of a mediocre element (see F. Yao[16]), which is defined, for our present purpose, to be an element with a rank in the middle third. That is, for any input set  $V = \{x_1, x_2, \ldots, x_n\}$ , we wish to find an element  $x_j$  such that  $n/3 \leq \ell_V(x_j) \leq 2n/3$ . For any fixed  $0 < \lambda < 1$ , it is not difficult to construct a randomized algorithm with error probability bounded by  $\lambda$  that uses only constant  $\log(1/\lambda)$  comparisons. Since any pure algorithm has to make  $2n/3$  comparisons in the worst case, this provides an example for our assertion. However, we do not have an analogous example where an errorless randomized algorithm performs much better than the worst-case complexity.

# 4. Concluding Remarks

We have developed a unified average complexity concept in some decision tree models, and demonstrated its usefulness. Many of these results have generalizations. For example, Theorem 4 can be extended to any string property whose invariant group is transitive. We list below some important unanswered questions.

(1) Despite the successful applications of randomization to several problems [1,11,13], there is little

proof that the randomized approach really lowers the computation time by order of magnitude (compared to the worst-case complexity of pure algorithms). It seems that the only concrete demonstration that exists in the literature, apart from our example in Section 3, is a result of Frevald cited in Gill's paper [3, revised version]. It states that the language  $\{ww|w\in \{0,l\}^{*}\}$  can be recognized by a l-tape Turing machine with error  $\lambda >0$  in  $O(n\log^2 n)$  steps (as compared with  $c\cdot n^2$  for a conventional l-tape Turing machine). There does not seem to be any similar example for an errorless randomized algorithm. Question: In our models, is there such an example?

(2) Is it true that  $\mathbf{F}_{\dot{\mathbf{i}}}(\mathbb{P}) \geq c \cdot n^{2}$  for all monotone graph properties? The corresponding question for the worst-case complexity was answered by Rivest and Vuillemin [12]. It is in general desirable to develop more lower bound techniques for  $\mathbf{F}_{\dot{\mathbf{i}}}(\mathbb{P})$ .

(3) With regard to Theorem 3, can one show a similar inequality in the opposite direction?

(4) Can one demonstrate non-linear lower bounds for 1-tape probabilistic Turing machines with error in concrete examples? A good candidate is the recognition of the language  $\mathbf{L} = \{\mathbf{wcw}^{\mathbf{R}}| \quad \mathbf{w} \in \{0,1\}^{*}\}$  (cf. [5] Theorem 10.7).

(5) The subject studied here shares certain common grounds with Game theory and statistical decision problems. It would be interesting to know of further connections.

# References



[1] J. Carter and M. Wegman, "Universal Classes of Hash Functions", Proc. 9th Annual ACM Symposium on Theory of Computing (1977), 106 - 112.





[2] R. Floyd and R. Rivest, "Expected Time Bounds for Selection", CACM 18 (1975), 165-172.





[3] J. Gill, "Computational Complexity of Probabilistic Turing Machines", Proc. 6th Annual ACM Symposium on Theory of Computing (1974), 91-95, revised Feb. 1977.





[4] M. Fredman, "How Good Is the Information Theory Bound?", Theoretical Computer Science 1 (1976), 355-361.





[5] J. Hopcroft and J. Ullman, Formal Languages and their Relation to Automata, Addison-Wesley(1969).





[6] R. Karp, "Probabilistic Analysis of Combinatorial Search", in Algorithms and Complexity, edited by J. Traub, Academic Press (1976), 1-20.





[7] Kirkpatrick, "Topics in the Complexity of Combinatorial Algorithms", University of Toronto Technical Report no. 74(1974).





[8] D. Knuth, The Art of Computer Programming vol 3, Addison-Wesley (1973).





[9] R. Luce and H. Raiffa, Games and Decisions, Wiley (1957).





[10] M. Rabin, "Probabilistic Algorithms", in Algorithms and Complexity, edited by J. Traub, Academic Press (1976), 21-40.





[11] I. Pohl, "Minimean Optimality in Sorting Algorithms" Proc. 16th Annual Symposium on Foundations of Computer Science (1975), 71-74.





[12] R. Rivest and J. Vuillemin, "On Recognizing Graph Properties From Adjacency Matrices", Theoretical Computer Science 3 (1976), 371-384.





[13] R. Solovay and V. Strassen, "Fast Monte-Carlo Test for Primality", SIAM J. on Computing 6(1977), 84-85.





[14] Von Neumann, "Zur Theorie der Gesellschaftsspiele", Math Annalen 100(1928), 295-320.





[15] A. Yao and F. Yao, "On the Average-Case Complexity of Selecting the t-th Best", to appear.





[16] F. Yao, "On Lower Bounds for Selection Problems", MIT Project Report TR-121 (1974).


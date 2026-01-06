# A Note on the Complexity of Cryptography

# GILLES BRASSARD

Abstract-Evidence is given for the difficulty of an eventual proof of computational security for cryptosystems based on one-way functions, such as the one proposed by Diffie and Hellman. A proof of NP-completeness for the cryptanalytic effort would imply  $\mathbf{NP} = \mathbf{CoNP}$ .

# I. INTRODUCTION

Diffie and Hellman [1] have proposed the use of the exponential function in a finite field for cryptographic purposes. This proposal is based on the conjecture that the inverse function, the logarithm, is not feasibly computable. The next best thing to a proof of this conjecture would be to show that the logarithm is NP-hard in the sense that there is a Turing machine using it as oracle that can accept some NP-complete set in polynomial time. If this were the case, we would know that the logarithm is hard indeed under the generally accepted assumption that  $P \neq \mathbf{NP}$  [2, ch. 10].

A word of caution is necessary here. Conventional complexity deals with worst case behavior: a function is said to be not feasibly computable if, for any algorithm  $A$  that computes it and any polynomial  $P$ , there is at least one input  $x$  on which  $A$  takes more than  $P(n)$  steps, where  $n$  is the length of  $x$ . That is not quite the notion needed in cryptography: it would be a poor cryptosystem that allows easy enemy decipherment of all but a few cryptograms. Nevertheless, it appears that even a proof that the logarithm is hard in the worst case escapes current techniques, let alone a proof of the computational security of Diffie and Hellman's proposed cryptosystem.

A nondeterministic Turing machine  $M$  is said to compute the function  $f$  if, for any input  $x$ , at least one path of the computation halts and if every halting path does so with  $f(x)$  on its output tape. Similarly  $M$  accepts a set  $S$  if, for any input  $x$ , there exists a computation path which halts (i.e., accepts) if and only if  $x \in S$ . The key observation is that it is possible to compute finite

Manuscript received April 28, 1978; revised September 11, 1978. This work was supported by the IBM Thomas J. Watson Research Center.

The author is with the Department of Computer Science, Cornell University, Ithaca NY 14850.

field logarithms in polynomial time using such a machine. As an application of a theorem by Miller [3], the projection  $P_{\log}$  of the logarithm function (defined below) belongs to  $\mathbf{NP} \cap \mathbf{CoNP}$ . Moreover,  $P_{\log} \in P$  if and only if the logarithm can be computed in deterministic polynomial time. A proof of Diffie and Hellman's conjecture would therefore imply that  $P \subsetneq \mathbf{NP} \cap \mathbf{CoNP}$  with  $P_{\log}$  as witness. Furthermore, should the logarithm be NP-hard, we would conclude that  $\mathbf{NP} = \mathbf{CoNP}$  because  $P_{\log}$  would be both NP-complete and a member of CoNP. More details follow. Since both these results  $(P \subsetneq \mathbf{NP} \cap \mathbf{CoNP}$  and  $\mathbf{NP} = \mathbf{CoNP})$  are expected to be either false or very difficult to establish, we conclude this is also the case for the security of the cryptosystem.

# II. CONSTRUCTION

In an attempt to make this section self-contained, we shall not use Miller's result [3] explicitly. The techniques used will however be similar to his. We shall also short-circuit the proof that the logarithm can be computed in polynomial time by a nondeterministic Turing machine.

Define the logarithm function  $\log (p,r,n)$  as follows: if  $p$  is a prime,  $r$  is a primitive root of  $p$  [4, sec. 4.5.4], and  $0 < n < p$ , then  $\log (p,r,n)$  is the unique  $m$  such that  $0 < m < p$  and  $r^m = n$  (mod  $p$ ). Otherwise  $\log (p,r,n)$  is zero. Define the projection  $P_{\log}$  as

$$
\{\langle p, r, n, t \rangle | \log (p, r, n) > t \}
$$

where  $\langle p, r, n, t \rangle$  is an abbreviation for  $\langle p, \langle r, \langle n, t \rangle \rangle$  and  $\langle \cdot, \cdot \rangle$  is a suitable pairing function.

$P_{\log} \in \mathbf{NP}$ :  $p$  is a prime and  $r$  is a primitive root of  $p$  if and only if  $r^{p-1} = 1 \pmod{p}$  and for each  $q$  a prime factor of  $p-1$ ,  $r^{(p-1)/q} \neq 1 \pmod{p}$  [4, sec. 4.5.4]. These conditions can be checked in nondeterministic polynomial time by guessing the prime decomposition of  $p-1$  together with certificates of primality [5] for each of the factors and by using a divide-and-conquer strategy to compute exponentials modulo  $p$  [4, sec. 4.6.3]. Once it is known that  $p$  is prime and  $r$  is a primitive root, assuming  $0 < n < p$ , the unique  $m$ ,  $0 < m < p$ , such that  $r^m = n \pmod{p}$  can be guessed. If  $m > t$ ,  $\langle p, r, n, t \rangle$  is in  $P_{\log}$ .

$P_{\log} \in \mathbf{CoNP}$ :  $\langle p, r, n, t \rangle$  is not in  $P_{\log}$  if and only if  $\log(p, r, n) \leqslant t$ . This is true if and only if either there are  $i$  and  $j$  ( $0 < i < j < p$ ) such that  $r^i = r^j \pmod{p}$ , there is an  $m \leqslant t$  such that  $r^m = n \pmod{p}$ , or it is not the case that  $0 < n < p$ . These conditions can be checked nondeterministically in polynomial time.

If  $P_{\log} \in P$ , then the logarithm can be computed deterministically in polynomial time by the following divide-and-conquer algorithm:

function  $\log (p,r,n)$

$i:=0$

$j:=p-1$

while  $i <   j$  do

$$
\begin{array}{l} / * i \leqslant \log \leqslant j * / \\ k := \lfloor (i + j) / 2 \rfloor \\ i := k + 1 \\ e l s e j := k f i \\ \end{array}
$$

od

return  $i$

end log.

Finally, should the logarithm be NP-hard, then so would  $P_{\log}$ , because the above algorithm shows that one can compute the logarithm efficiently given  $P_{\log}$ . An oracle for  $P_{\log}$  can therefore be used to simulate an oracle for the logarithm.  $P_{\log}$ , being in NP, would be NP-complete. However,  $P_{\log} \in \mathbf{CoNP}$ . We conclude that  $\mathbf{NP} = \mathbf{CoNP}$ , for otherwise there could be no NP-complete sets the complement of which are in NP. We give a proof of this claim in the Appendix.

# III. GENERALIZATION

The reasoning above can be generalized to other cryptosystems based on one-way functions. A one-way function, as defined in [1], is a function  $f$  such that, for any argument  $x$  in the domain of  $f$ , it is easy to compute the corresponding value  $f(x)$ , yet, for almost all  $y$  in the range of  $f$ , it is computationally infeasible to solve the equation  $y = f(x)$  for any suitable argument  $x$ . So far we have used a candidate for one-way functions set forth by Diffie and Hellman which is the exponentiation in a finite field.

It turns out that if any function  $f$ , satisfying a few restrictions, can be proved to be one-way, then  $P \not\equiv \mathbf{NP} \cap \mathbf{CoNP}$ . Similarly, if evidence is given that  $f$  is one-way by showing its inverse to be NP-hard, then  $\mathbf{NP} = \mathbf{CoNP}$ . The restrictions are that  $f$  be one-one from an NP domain onto a CoNP range and that there be a polynomial  $P$  such that, for any  $x$  in the range of  $f$ ,  $|x| < P(|f(x)|)$ , where  $|x|$  denotes the length of the binary representation of  $x$ .

This leads us to a final example. Rivest, Shamir, and Adleman [6] have proposed a public-key cryptosystem based on the belief that the function multiplication is one-way when restricted to prime numbers. In more conventional terms, it is easy to multiply two prime numbers, but we as yet do not know how to efficiently find the factors of a large number even with the foreknowledge that it is the product of two primes. Here again it turns out that a proof of computational security for their cryptosystem would imply that  $P \not\subsetneq \mathbf{NP} \cap \mathbf{CoNP}$  while a proof of NP-hardness for the cryptanalytic effort would imply that  $\mathbf{NP} = \mathbf{CoNP}$ . For a direct proof of these results, mimic the proof of Section II replacing  $P_{\log}$  by  $S$ , which is defined as

$$
\{\langle x, y \rangle | x \text {h a s a p r i m e f a c t o r s m a l l e r t h a n} y \}.
$$

As in Section II, one proves that  $S \in \mathbf{NP} \cap \mathbf{CoNP}$  and that  $S \in \pmb{P}$  if and only if prime decomposition is feasibly computable.

# ACKNOWLEDGMENT

Similar results have been found independently by Leonard Adleman, Ronald Rivest, and Gary Miller [7].

# APPENDIX

We shall prove that if a set  $A$  is NP-complete and if  $A \in \mathbf{CoNP}$ , then  $\mathbf{NP} = \mathbf{CoNP}$ . This is obvious for Karp's notion of NP-completeness [8] but requires proof for Cook's notion [9], which we have used throughout this correspondence. Let  $M+$  and  $M-$  be nondeterministic polynomial-time-bounded Turing machines that accept  $A$  and its complement, respectively.

For any  $L \in \mathbf{NP}$ , there is a deterministic polynomial-time-bounded Turing machine  $M$  which accepts  $L$  given an oracle for  $A$ . Consider the nondeterministic Turing machine  $M'$ , which, on any input, deterministically simulates  $M$  step by step except when  $M$  asks a question of the oracle. In such a case,  $M'$  guesses whether the answer ought to be "yes" or "no" and nondeterministically simulates either  $M +$  or  $M -$  depending on this choice. Should  $M'$  reach an accepting state of  $M +$  or  $M -$ , it would know it is on the right track and would resume the deterministic simulation of  $M$  in the appropriate oracle answer state. Should  $M'$  reach a rejecting state of  $M +$  or  $M -$  instead, it would know nothing at all and would immediately reject the original input. Finally, when  $M$  reaches a final state,  $M'$  accepts if and only if  $M$  rejects.

It is obvious that  $M'$  runs in polynomial time and that it accepts the complement of  $L$ , so that  $L \in \mathbf{CoNP}$ . This proves that  $\mathbf{NP} \subseteq \mathbf{CoNP}$ . Now, given any  $L \in \mathbf{CoNP}$ , its complement is in  $\mathbf{NP}$  by definition of  $\mathbf{CoNP}$  and hence in  $\mathbf{CoNP}$ , since  $\mathbf{NP} \subseteq \mathbf{CoNP}$ .  $L \in \mathbf{NP}$  again by definition of  $\mathbf{CoNP}$ . This shows that  $\mathbf{CoNP} \subseteq \mathbf{NP}$  and completes the proof that  $\mathbf{NP} = \mathbf{CoNP}$ .

# REFERENCES



[1] W. Diffie and M. E. Hellman, “New directions in cryptography,” IEEE Trans. Inform. Theory, vol. IT-22, pp. 644–654, Nov. 1976.





[2] A. V. Aho, J. E. Hopcroft, and J. D. Ullman, The Design and Analysis of Computer Algorithms. Reading, MA: Addison-Wesley, 1974.





[3] G. L. Miller, “Riemann's hypothesis and tests for primality,” J. Comput. Syst. Sci., vol. 13, pp. 300-317, 1976.





[4] D. E. Knuth, The Art of Computer Programming, vol. 2, Semi-Numerical Algorithms. Reading, MA: Addison-Wesley, 1969.





[5] V. Pratt, "Every prime has a succinct certificate," SIAM J. Comput., vol. 4, pp. 214-220, 1975.





[6] R. Rivest, A. Shamir, and L. Adleman, “A method of obtaining digital signatures and public-key cryptosystem,” Commun. Ass. Comput. Mach., vol. 21, pp. 120–126, Feb. 1978.





[7] L. Adleman, private communication, 1978.





[8] R. M. Karp, "Reducibility among combinatorial problems," in Complexity of Computer Computations, R. E. Miller and J. W. Thatcher, Eds. NY: Plenum, 1972.





[9] S. A. Cook, “The complexity of theorem proving procedures,” in Proc. 3rd Ann. ACM Symp. Theory of Computing, 1971, pp. 151-158.




# Mathematics

<h3>Table of Contents</h3>

[TOC]

## Theory Terminology

- A theorem is a statement that has been proven to be true, either on the basis of generally accepted statements such as axioms, or on the basis of previously established statements.
- An axiom or postulate is a statement that is accepted without proof and regarded as fundamental to a subject. Historically axioms were regarded as "self-evident", but recently they have been considered assumptions that characterize the subject of study. In classical geometry, axioms are general statements, while postulates are statements about geometrical objects.[17] A definition is yet another form of statement that is also accepted without proof — since it simply gives the meaning of a word or phrase in terms of known concepts.
- A conjecture (or sometimes hypothesis, but with a different meaning from the one discussed above) is an unproved statement that is believed to be true. To be considered a conjecture, a statement must usually be proposed publicly, at which point the name of the proponent may be attached to the conjecture, as with Goldbach's conjecture. Other famous conjectures include the Collatz conjecture and the Riemann hypothesis. On the other hand, Fermat's Last Theorem has always been known by that name, even before it was proved; it was never known as "Fermat's conjecture".
- A proposition is a theorem of lesser importance, or considered so elementary that it may be stated with no proof. It is also the term for the statement-part of the theorem (If A then B) that precedes the proof-part, and particularly elementary theorems are often given only as a proposition, hence the name. This term connotes a statement with an especially simple or immediately obvious proof, while the term theorem is usually reserved for the most important results or those with long or difficult proofs. Some authors never use the word "proposition", while some others reserve the word "theorem" only for fundamental, central, or particularly important results.[a]
- A lemma is a "helping theorem", a proposition with little applicability except that it forms part of the proof of a larger theorem. In some cases, as the relative importance of different theorems becomes more clear, what was once considered a lemma is now considered a theorem, though the word "lemma" remains in the name. Examples include Gauss's lemma, Zorn's lemma, and the fundamental lemma.
- A corollary is a proposition that follows with little or no required proof from another theorem or definition.[18] Also a corollary can be a theorem restated in a simpler form, for a more restricted special case. For example, the theorem that all angles in a rectangle are right angles has as corollary that all angles in a square (a special case of a rectangle) are right angles.
- An Inference: 
- A converse of a theorem is a statement formed by interchanging what is given in a theorem and what is to be proved. For example, the isosceles triangle theorem states that if two sides of a triangle are equal then two angles are equal. In the converse, the given (that two sides are equal) and what is to be proved (that two angles are equal) are swapped, so the converse is the statement that if two angles of a triangle are equal then two sides are equal. In this example, the converse can be proved as another theorem, but this is often not the case. For example, the converse to the theorem that two right angles are equal angles is the statement that two equal angles must be right angles, and this is clearly not always the case.[19]
- A generalization is a theorem which includes a previously proved theorem as a special case and hence as a corollary.[b]
- An identity is an equality, contained in a theorem, between two mathematical expressions that holds regardless of the values being used for any variables or parameters appearing in the expressions (as long as they are within the range of validity).[20] Examples include Euler's formula and Vandermonde's identity.
- A rule is a theorem, such as Bayes' rule and Cramer's rule, that establishes a useful formula.
- A law or a principle is a theorem that applies in a wide range of circumstances. Examples include the law of large numbers, the law of cosines, Kolmogorov's zero–one law, Harnack's principle, the least-upper-bound principle, and the pigeonhole principle.[21]

## Arithmetic Progrssion

### Intro

Lets take series
1, 3, 5, 9, ..... nth

here 1, 1+2, 1 + (2+2), 1 + (2+2+2), .....  

    i.e. a + a+d, a+2d, a+3d,......
for n series  

    a + a+d, a+2d, a+3d,......, a + (n-1)d  
    

So,  

    a = initial number == 1  
    
    d = difference == 2  
    
nth or last term =  $l = a + (n-1)d$
    
    
**Sum of AP**  
= sum of a + a+d, a+2d, a+3d,......, a + (n-1)d  
= a + a+d + a+2d + a+3d + ......+ a+(n-1)d  
= a*n + d(1 + 2 + 3 +....+ n-1)  

i.e.  
>    $S_n = an + \frac{d(n-1)n}{2}$  

>    $S_n = \frac{1}{2}n(2a+ (n-1)d)$  

>    $S_n = \frac{1}{2}n(a+l)$


## Geometric Progression

### Intro

Lets take a series

> $2, 6, 18, 54, ....$

i.e.  
> $2, 2 \times 3, 2 \times 3^2, 2 \times 3^3, ...$

> $a,  a \times r,  2 \times r^2,  2 \times r^3, ...$

where
> $a$ is first term, and  
> $r$ is ratio  

So,
> $n^{th}$ term = $a \times r^{n-1}$ 

** Sum of the GP**

$S_n = a +  a  r +  2  r^2 +  2  r^3 + ... +  a  r^{n-1}$  
$rS_n = a  r +  2  r^2 +  2  r^3 + 2 r^4 + ... +  a r^{n}$  
$-------------------$
$S_n - rS_n = a - a r^n$  
$S_n (1 - r) = a (1 - r^n)$  
$S_n  = \frac{a (1 - r^n)}{(1 - r)}$  
$S_{\infty}  = \frac{a} {(1 - r)}$  

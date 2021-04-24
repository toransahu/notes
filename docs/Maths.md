[TOC]

# Maths

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

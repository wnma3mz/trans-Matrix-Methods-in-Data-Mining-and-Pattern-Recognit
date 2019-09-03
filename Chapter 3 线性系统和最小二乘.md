# 第三章 线性系统和最小二乘

$A x = b$

$A \in \mathbb { R } ^ { n \times n }$

$A \in \mathbb { R } ^ { n \times n }$

$A ^ { ( 1 ) } : = L _ { 1 } ^ { - 1 } P _ { 1 } A$

$L _ { 1 } = \left( \begin{array} { c c } { 1 } & { 0 } \\ { m _ { 1 } } & { I } \end{array} \right) , \quad m _ { 1 } = \left( \begin{array} { c } { m _ { 21 } } \\ { m _ { 31 } } \\ { \vdots } \\ { m _ { n 1 } } \end{array} \right)$

$A ^ { ( 1 ) } = \left( \begin{array} { c c c c } { a _ { 11 } ^ { \prime } } & { a _ { 12 } ^ { \prime } } & { \dots } & { a _ { 1 n } ^ { \prime } } \\ { 0 } & { a _ { 22 } ^ { ( 1 ) } } & { \cdots } & { a _ { 2 n } ^ { ( 1 ) } } \\ { \vdots } & { } & { } \\ { 0 } & { a _ { n 2 } ^ { ( 1 ) } } & { \dots } & { a _ { n n } ^ { ( 1 ) } } \end{array} \right)$

$P A = L U$

$P _ { 1 } A = L _ { 1 } A ^ { ( 1 ) }$

$B = \left( \begin{array} { c c c } { a _ { 22 } ^ { ( 1 ) } } & { \dots } & { a _ { 2 n } ^ { ( 1 ) } } \\ { \vdots } & { } & { } \\ { a _ { n 2 } ^ { ( 1 ) } } & { \cdots } & { a _ { n n } ^ { ( 1 ) } } \end{array} \right)$

$P _ { B } B = L _ { B } U _ { B }$

$P A = L U$

$U = \left( \begin{array} { c c } { a _ { 11 } ^ { \prime } } & { a _ { 2 } ^ { T } } \\ { 0 } & { U _ { B } } \end{array} \right) , \quad L = \left( \begin{array} { c c } { 1 } & { 0 } \\ { P _ { B } m _ { 1 } } & { L _ { B } } \end{array} \right) , \quad P = \left( \begin{array} { c c } { 1 } & { 0 } \\ { 0 } & { P _ { B } } \end{array} \right) P _ { 1 }$

$a _ { 2 } ^ { T } = \left( a _ { 12 } ^ { \prime } a _ { 13 } ^ { \prime } \ldots a _ { 1 n } ^ { \prime } \right)$

$2 \sum\limits_ { k = 1 } ^ { n - 1 } ( n - k + 1 ) ^ { 2 } \approx \frac { 2 n ^ { 3 } } { 3 }$

$A = L D L ^ { T }$

$A = \left( \begin{array} { l l l } { 8 } & { 4 } & { 2 } \\ { 4 } & { 6 } & { 0 } \\ { 2 } & { 0 } & { 3 } \end{array} \right)$

$A = L U = \left(\begin{array} { c c c } { 1 } & { 0 } & { 0 } \\ { 0.5 } & { 1 } & { 0 } \\ { 0.25 } & { -0.25 } & { 1 } \end{array} \right) \left(\begin{array} { c c c } { 8 } & { 4 } & { 2 } \\ { 0 } & { 4 } & { -1 } \\ { 0 } & { 0 } & { 2.25 } \end{array} \right)$

$A = L D L ^ { T } , \quad D = \left(\begin{array} { c c c } { 8 } & { 0 } & { 0 } \\ { 0 } & { 4 } & { 0 } \\ { 0 } & { 0 } & { 2.25 } \end{array} \right)$

$D ^ { 1 / 2 } = \left( \begin{array} { c c c c } { \sqrt { d _ { 1 } } } & { } & { } & { } \\ { } & { \sqrt { d _ { 2 } } } & { } & { } \\ { } & { } & { \ddots } & { } \\ { } & { } & { } & { \sqrt { d _ { n } } } \end{array} \right)$

$A = L D L ^ { T } = \left( L D ^ { 1 / 2 } \right) \left( D ^ { 1 / 2 } L ^ { T } \right) = U ^ { T } U$

$\kappa ( A ) = \| A \| \left\| A ^ { - 1 } \right\|$

$\kappa _ { 2 } ( A ) = \| A \| _ { 2 } \left\| A ^ { - 1 } \right\| _ { 2 }$

$\| \delta A \| \left\| A ^ { - 1 } \right\| = r < 1$

$A + \delta A$

$\left\| ( A + \delta A ) ^ { - 1 } \right\| \leq \frac { \left\| A ^ { - 1 } \right\| } { 1 - r }$

$( A + \delta A ) y = b + \delta b$

$\frac { \| y - x \| } { \| x \| } \leq \frac { \kappa ( A ) } { 1 - r } \left( \frac { \| \delta A \| } { \| A \| } + \frac { \| \delta b \| } { \| b \| } \right)$

$f l [ x ] = x ( 1 + \epsilon ) , \quad | \epsilon | \leq \mu$

$f l \left[ a _ { i j } \right] = a _ { i j } \left( 1 + \epsilon _ { i j } \right) , \quad \left| \epsilon _ { i j } \right| \leq \mu$

$f l [ A ] = A + \delta A , \quad f l [ b ] = b + \delta b$

$\| \delta A \| _ { \infty } \leq \mu \| A \| _ { \infty } , \quad \| \delta b \| _ { \infty } \leq \mu \| b \| _ { \infty }$

$( A + \delta A ) \widehat { x } = b + \delta b$

$\widehat { x }$

$\frac { \| \widehat { x } - x \| _ { \infty } } { \| x \| _ { \infty } } \leq \frac { \kappa _ { \infty } ( A ) } { 1 - r } 2 \mu$

$r = \mu \kappa _ { \infty } ( A ) < 1$

$\widehat { L } \widehat { y } = P b , \quad \widehat { R } \widehat { x } = \widehat { y }$

$( A + \delta A ) \widehat { x } = b$

$\| \delta A \| _ { \infty } \leq k ( n ) g _ { n } \mu \| A \| _ { \infty } , \quad g _ { n } = \frac { \max _ { i , j , k } \left| \widehat { a } _ { i j } ^ { ( k ) } \right| } { \max _ { i , j } \left| a _ { i j } \right| }$

$\widehat { a } _ { i j } ^ { ( k ) }$

$a _ { i j } = 0 \text { if } j - i > p \text { or } i - j > q$

$A = \left( \begin{array} { c c c c c c } { a _ { 11 } } & { a _ { 12 } } & { 0 } & { 0 } & { 0 } & { 0 } \\ { a _ { 21 } } & { a _ { 22 } } & { a _ { 23 } } & { 0 } & { 0 } & { 0 } \\ { a _ { 31 } } & { a _ { 32 } } & { a _ { 33 } } & { a _ { 34 } } & { 0 } & { 0 } \\ { 0 } & { a _ { 42 } } & { a _ { 43 } } & { a _ { 44 } } & { a _ { 45 } } & { 0 } \\ { 0 } & { 0 } & { a _ { 53 } } & { a _ { 54 } } & { a _ { 55 } } & { a _ { 56 } } \\ { 0 } & { 0 } & { 0 } & { a _ { 64 } } & { a _ { 65 } } & { a _ { 66 } } \end{array} \right)$

$A = \left( \begin{array} { c c c c c c } { \alpha _ { 1 } } & { \beta _ { 1 } } & { } & { } & { } \\ { \gamma _ { 2 } } & { \alpha _ { 2 } } & { \beta _ { 2 } } & { } & { } \\ { } & { \gamma _ { 3 } } & { \alpha _ { 3 } } & { \beta _ { 3 } } \\ { } & { } & { } & { } \\ { } & { } & { \ddots } & { \ddots } & { \ddots } \\ { } & { } & { } & { \gamma _ { n - 1 } } & { \alpha _ { n - 1 } } & { \beta _ { n - 1 } } \\ { } & { } & { } & { \gamma _ { n } } & { } & { \alpha _ { n } } \end{array} \right)$



```matlab
% LU Decomposition of a Tridiagonal Matrix.
for k=1:n-1
  gamma(k+1)=gamma(k+1)/alpha(k);
  alpha(k+1)=alpha(k+1)*beta(k);
end
% Forward Substitution for the Solution of Ly = b.
y(1)=b(1);
for k=2:n
  y(k)=b(k)-gamma(k)*y(k-1);
end
% Back Substitution for the Solution of Ux = y.
x(n)=y(n)/alpha(n);
for k=n-1:-1:1
  x(k)=(y(k)-beta(k)*x(k+1))/alpha(k);
end
```



$A = \left( \begin{array} { c c c c c } { 4 } & { 2 } & { } & { } & { } \\ { 2 } & { 5 } & { 2 } & { } & { } \\ { } & { 2 } & { 5 } & { 2 } & { } \\ { } & { } & { 2 } & { 5 } & { 2 } \\ { } & { } & { } & { 2 } & { 5 } \end{array} \right)$





$U = \left( \begin{array} { c c c c c } { 2 } & { 1 } & { } & { } & { } \\ { } & { 2 } & { 1 } & { } & { } \\ { } & { } & { 2 } & { 1 } & { } \\ { } & { } & { } & { 2 } & { 1 } \\ { } & { } & { } & { } & { 2 } \end{array} \right)$

$A ^ { - 1 } = \frac { 1 } { 2 ^ { 10 } } \left( \begin{array} { c c c c c } { 341 } & { - 170 } & { 84 } & { - 40 } & { 16 } \\ { - 170 } & { 340 } & { - 168 } & { 80 } & { - 32 } \\ { 84 } & { - 168 } & { 336 } & { - 160 } & { 64 } \\ { - 40 } & { 80 } & { - 160 } & { 320 } & { - 128 } \\ { 16 } & { - 32 } & { 64 } & { - 128 } & { 256 } \end{array} \right)$

$e + \kappa F = l$

$\frac { \mathrm { F } } { 1 } \frac { 1 } { 7.97 } \frac { 2 } { 10.2 } \frac { 3 } { 14.2 } \frac { 4 } { 16.0 } \frac { 5 } { 21.2 }$

$\begin{array} { l } { e + \kappa 1 = 7.97 } \\ { e + \kappa 2 = 10.2 } \\ { e + \kappa 3 = 14.2 } \\ { e + \kappa 4 = 16.0 } \\ { e + \kappa 5 = 21.2 } \end{array}$

$\left(\begin{array} { l l } { 1 } & { 1 } \\ { 1 } & { 2 } \\ { 1 } & { 3 } \\ { 1 } & { 4 } \\ { 1 } & { 5 } \end{array} \right) \left(\begin{array} { l } { e } \\ { \kappa } \end{array} \right) = \left(\begin{array} { c } { 7.97 } \\ { 10.2 } \\ { 14.2 } \\ { 16.0 } \\ { 21.2 } \end{array} \right)$

$A \in \mathbb { R } ^ { m \times n } , m > n$

$x _ { 1 } a _ { \cdot 1 } + x _ { 2 } a _ { \cdot 2 } = b$

$x _ { 1 } a _ { \cdot 1 } + x _ { 2 } a _ { \cdot 2 } = b$

$r = b - x _ { 1 } a _ { 1 } - x _ { 2 } a _ { \cdot 2 } = b - A x$

$\min\limits_ { x } \| b - A x \| _ { 2 }$

$r ^ { T } a _ { \cdot j } = 0 , \quad j = 1,2 , \ldots , n$

$r ^ { T } \left(\begin{array} { c c c c } { a _{ .1 } } & { a _{ .2 } } & { \cdots } & { a _{ . n } } \end{array} \right) = r ^ { T } A = 0$

$r = b - A x$

$A ^ { T } A x = A ^ { T } b$

$A ^ { T } A x = A ^ { T } b$

$x ^ { T } A ^ { T } A x = y ^ { T } y = \sum\limits_ { i = 1 } ^ { n } y _ { i } ^ { 2 } > 0$

$r = b - A x$

$r = b - A \widehat { x } + A ( \widehat { x } - x ) = \widehat { r } + A ( \widehat { x } - x )$

$\begin{aligned} \| r \| _ { 2 } ^ { 2 } & = r ^ { T } r = ( \widehat { r } + A ( \widehat { x } - x ) ) ^ { T } ( \widehat { r } + A ( \widehat { x } - x ) ) \\ & = \widehat { r } ^ { T } \widehat { r } + \widehat { r } ^ { T } A ( \widehat { x } - x ) + ( \widehat { x } - x ) ^ { T } A ^ { T } \widehat { r } + ( \widehat { x } - x ) ^ { T } A ^ { T } A ( \widehat { x } - x ) \end{aligned}$

$A ^ { T } \widehat { r } = 0$

$\| r \| _ { 2 } ^ { 2 } = \widehat { r } ^ { T } \widehat { r } + ( \widehat { x } - x ) ^ { T } A ^ { T } A ( \widehat { x } - x ) = \| \widehat { r } \| _ { 2 } ^ { 2 } + \| A ( \widehat { x } - x ) \| _ { 2 } ^ { 2 } \geq \| \widehat { r } \| _ { 2 } ^ { 2 }$

$A = \left(\begin{array} { c c c } { 1 } & { 1 } & { 1 } \\ { 1 } & { 2 } \\ { 1 } & { 3 } \\ { 1 } & { 41 } & { 5 } \end{array} \right) , \quad b = \left(\begin{array} { c } { 7.97 } \\ { 10.2 } \\ { 14.2 } \\ { 16.021 .2 } \end{array} \right)$

```matlab
>> C=A’*A % Normal equations

C = 5 15
    15 55
    
>> x=C\(A’*b)

x = 4.2360
    3.2260
```

$\kappa\left(A^{T} A\right)=(\kappa(A))^{2}$

$A=\left(\begin{array}{ll}{1} & {1} \\ {\epsilon} & {0} \\ {0} & {\epsilon}\end{array}\right)$

$A^{T} A=\left(\begin{array}{cc}{1+\epsilon^{2}} & {1} \\ {1} & {1+\epsilon^{2}}\end{array}\right)$

$1+\epsilon^{2}$

$f l\left[1+\epsilon^{2}\right]=1$

```matlab
A = 1 1
    1 2
    1 3
    1 4
    1 5
    
cond(A) = 8.3657

cond(A’*A) = 69.9857
```

$l(x)=c_{0}+c_{1} x$

$x=(101 \quad 102 \quad 103 \quad 104 \quad 105)^{T}$

```matlab
A = 1 101
    1 102
    1 103
    1 104
    1 105
    
cond(A) = 7.5038e+03

cond(A’*A) = 5.6307e+07
```

$l(x)=b_{0}+b_{1}(x-103)$

$\min _{x_{i}}\left\|A x_{i}-b_{i}\right\|_{2}, \quad i=1,2, \ldots, p$

$X=\left(\begin{array}{llll}{x_{1}} & {x_{2}} & {\dots} & {x_{p}}\end{array}\right)$

$X=\left(\begin{array}{llll}{b_{1}} & {b_{2}} & {\ldots} & {b_{p}}\end{array}\right)$

$\min _{X}\|A X-B\|_{F}$

$X=\left(A^{T} A\right)^{-1} A^{T} B$

$\|A X-B\|_{F}^{2}=\sum_{i=1}^{p}\left\|A x_{i}-b_{i}\right\|_{2}^{2}$


# 第二章 向量和矩阵

我们将假设读者已知线性代数的基本概念。为了完整起见，这里将概括一些。

## 2.1 矩阵-向量乘法

如何定义线性代数中的基本操作很重要，因为它会影响一个人对抽象概念的心理图像。有时人们会认为操作应该以某种顺序完成，而事实上*这样的定义*并没有排序$^3$。 设 $A$ 是 $m\times n$矩阵。考虑矩阵-向量乘法的定义：

$y = A x , \quad y _ { i } = \sum _ { j = 1 } ^ { n } a _ { i j } x _ { j } , \quad i = 1 , \ldots , m$ ，式2.1

这可以用符号来说明

$\left( \begin{array} { l } { \times } \\ { \times } \\ { \times } \\ { \times } \end{array} \right)=\left( \begin{array} { c c c c } { \leftarrow } & { - } & { - } & { \rightarrow } \\ { \leftarrow } & { - } & { - } & { \rightarrow } \\ { \leftarrow } & { - } & { - } & { \rightarrow } \\ {\leftarrow } & { - } & { - } & { \rightarrow } \end{array} \right) \left( \begin{array} { l } { \uparrow } \\ { | } \\ { | }  \\ { \downarrow } \end{array} \right)$，式2.2

显然，向量 $y$ 的不同分量的计算完全彼此独立，并且可以以任何顺序完成。但是，定义可能导致人们认为应该按行访问矩阵，如（2.2）和以下 MATLAB 代码所示：

```matlab
for i=1:m
  y(i)=0;
  for j=1:n
    y(i)=y(i)+A(i,j)*x(j);
  end
end
```

$^3$重要的是要意识到，在具有内存层次结构的现代计算机上，执行操作的顺序通常对性能至关重要。但是，我们不会本书追求这方面。

或者，我们可以按以下方式编写操作。设 $a_{·j}$ 为 $A$ 的列向量。然后我们就可以写成

$y = A x = \left(\begin{array} { c c c c } { a _{ 1 } } & { a _{ .2 } } & { \cdots } & { a _{ . n } } \end{array} \right) \left(\begin{array} { c } { x _{ 1 } } \\ { x _{ 2 } } \\ { \vdots } \\ { x _{ n } } \end{array} \right) = \sum\limits_{ j = 1 } ^ { n } x _{ j } a _{ . . j }$

这可以用符号说明：

$\left( \begin{array} { l } { \uparrow } \\ { | } \\ { | }  \\ { \downarrow } \end{array} \right)=\left( \begin{array} { l l l l } { \uparrow } & { \uparrow } & { \uparrow } & { \uparrow } \\ { | } & { | } & { | } & { | } \\ { | } & { | } & { | } & { | } \\ { \downarrow } & { \downarrow } & { \downarrow } & { \downarrow } \end{array} \right)\left( \begin{array} { l } { \times } \\ { \times } \\ { \times } \\ { \times } \end{array} \right) $，式2.3

在这里，向量是按列访问的。在MATLAB中，可以写成如下形式$^4$

```matlab
for i=1:m
    y(i)=0;
end
for j=1:n
    for i=1:m
    	y(i)=y(i)+A(i,j)*x(j);
    end
end
```

同样的，使用MATLAB中的向量计算

```matlab
y(1:m)=0;
for j=1:n
	y(1:m)=y(1:m)+A(1:m,j)*x(j);
end
```

因此，运行矩阵向量乘法的两种方法对应于代码中循环的顺序。这种书写方式还强调 $A$ 的列向量作为*基向量*，$x$ 的分量作为相对于基*坐标*的视图。

$^4$在LAPACK [1]的术语中，这是矩阵向量乘法的SAXPY版本。SAXPY是Basic Linear Algebra Subroutine（BLAS）库的首字母缩略词。

## 2.2 矩阵乘法

矩阵乘法可以用几种方式进行，每种方式表示矩阵的不同访问模式。设 $A \in \mathbb { R } ^ { m \times k }$ 和 $B \in \mathbb { R } ^ { k \times n }$，矩阵乘法的定义是

$\begin{aligned} \mathbb { R } ^ { m \times n } \ni C & = A B = \left( c _ { i j } \right) \\ c _ { i j } & = \sum _ { s = 1 } ^ { k } a _ { i s } b _ { s j } , \quad i = 1 , \ldots , m , \quad j = 1 , \ldots , n \end{aligned}$，式2.4

与矩阵向量乘法（2.1）的定义相比，我们发现在矩阵乘法中，B中的*每列向量*都*乘*以A。我们可以将（2.4）转换为矩阵乘法代码。


```matlab
for i=1:m
  for j=1:n
    for s=1:k
      C(i,j)=C(i,j)+A(i,s)*B(s,j)
    end
  end
end
```

这是矩阵乘法的内积版本，在下面的等效代码中强调了这一点：

```matlab
for i=1:m
  for j=1:n
	C(i,j)=A(i,1:k)*B(1:k,j)
  end
end
```

可以明显看到循环变量排列与 $3!=6$ 种不同的方法，我们可以编写一个*通用矩阵乘法*代码：

```matlab
for ...
  for ...
    for ...
      C(i,j)=C(i,j)+A(i,s)*B(s,j)
    end
  end
end
```

面向列（或SAXPY）的版本如下

```matlab
for j=1:n
  for s=1:k
	C(1:m,j)=C(1:m,j)+A(1:m,s)*B(s,j)
  end
end
```

矩阵 $A$ 由列访问，$B$ 由标量访问。此访问模式可以如图所示

$\left( \begin{array} { c } & & { \uparrow }&   \\ && { | }&  \\&& { | } & \\ & &  { \downarrow }& \end{array} \right)=\left( \begin{array} { l l l l } { \uparrow } & { \uparrow } & { \uparrow } & { \uparrow } \\ { | } & { | } & { | } & { | } \\ { | } & { | } & { | } & { | } \\ { \downarrow } & { \downarrow } & { \downarrow } & { \downarrow } \end{array} \right)\left( \begin{array} { l } && { \times }& \\ &&{ \times }& \\&& { \times }& \\ & &{ \times }& \end{array} \right) $

在另一种排列中，我们让s循环在外层的：


```matlab
for s=1:k
  for j=1:n
	C(1:m,j)=C(1:m,j)+A(1:m,s)*B(s,j)
  end
end
```

这可以解释为如下。设 $a_{.k}$ 表示 $A$ 的列向量，设 $b_k^T$ 作为 $B$ 的行向量，则矩阵乘法可写成

$C = A B = \left( \begin{array} { l l l l } { a _ { \cdot 1 } } & { a _ { 2 } } & { \ldots } & { a _ { k } } \end{array} \right)\left( \begin{array} { c } { b _ { 1 } ^ { T } } \\ { b _ { 2 } ^ { T } } \\ { \vdots } \\ { b _ { k } ^ { T } } \end{array} \right) = \sum\limits_ { s = 1 } ^ { k } a \cdot _ { s } b _ { s } ^ { T }$，式2.5

这是矩阵乘法的*外积*形式。记住，外积遵循矩阵乘法的标准定义：让 $x$ 和 $y$ 分别是 $\mathbb{R}^m$ 和 $\mathbb{R}^n$ 中的列向量；然后

$\begin{array}x y ^ { T } &= \left( \begin{array} { c } { x _ { 1 } } \\ { x _ { 2 } } \\ { \vdots } \\ { x _ { m } } \end{array} \right) \left( \begin{array} { c c c c } { y _ { 1 } } & { y _ { 2 } } & { \cdots } & { y _ { n } } \end{array} \right) = \left( \begin{array} { c c c c } { x _ { 1 } y _ { 1 } } & { x _ { 1 } y _ { 2 } } & { \cdots } & { x _ { 1 } y _ { n } } \\ { x _ { 2 } y _ { 1 } } & { x _ { 2 } y _ { 2 } } & { \cdots } & { x _ { 2 } y _ { n } } \\ { \vdots } & { \vdots } & { } & { \vdots } \\ { x _ { m } y _ { 1 } } & { x _ { m } y _ { 2 } } & { \cdots } & { x _ { m } y _ { n } }  \end{array}  \right) \\&= \left( \begin{array} { c c c c } { y _ { 1 } x } & { y _ { 2 } x } & { \cdots } & { y _ { n } x } \end{array} \right) = \left( \begin{array} { c } { x _ { 1 } y ^ { T } } \\ { x _ { 2 } y ^ { T } } \\ { \vdots } \\ { x _ { m } y ^ { T } } \end{array} \right)\end{array}$

在外积形式（2.5）中矩阵 $C=AB$ 可被视为简单矩阵 $a_{.s}b_{s.}^T$ 中 $C$ 的*展开式*。稍后我们将看到这样的矩阵的*秩*等于1。

## 2.3 内积和向量范数

在本节中，我们将简要讨论如何计算向量的“大小”。最常见的向量规范是

$\| x \| _ { 1 } = \sum _ { i = 1 } ^ { n } \left| x _ { i } \right|$

$\| x \| _ { 2 } = \sqrt { \sum\limits_ { i = 1 } ^ { n } x _ { i } ^ { 2 } }$

$\| x \| _ { \infty } = \max _ { 1 \leq i \leq n } \left| x _ { i } \right|$

欧几里得向量范数是 $\mathbb{R}^3$ 到 $ \mathbb{R}^n$ 中标准欧几里得距离的推广。这里定义的三个规范都是 $p$-norm的特殊情况：

$\| x \| _ { p } = \left( \sum _ { i = 1 } ^ { n } \left| x _ { i } \right| ^ { p } \right) ^ { 1 / p }$

与欧几里得向量范数相关联的是 $\mathbb{R}^n$ 中两个向量 $x$ 和 $y$ 之间的*内积*，定义为

$( x , y ) = x ^ { T } y$

一般来说，*向量范数*是一个具有以下性质的映射$\mathbb{R}^n\rightarrow\mathbb{R}$

$\| x \| \geq 0$

$\| x \| = 0$

$\| \alpha x \| = | \alpha | \| x \| , \alpha \in \mathbb { R }$

$\| x + y \| \leq \| x \| + \| y \|$

通过范数，我们可以引入向量的近似中连续性和误差的概念。假设 $\bar{x}$ 是向量 $x$ 的近似值。对于任何给定的向量范数，我们定义*绝对误差*。

$\| \delta x \| = \| \overline { x } - x \|$

及其*相对误差*（假设 $x\neq 0$）

$\frac { \| \delta x \| } { \| x \| } = \frac { \| \overline { x } - x \| } { \| x \| }$

在有限维向量空间中，所有向量范数在以下意义上都是等价的：对于任意两个范数 $||\cdot||_{\alpha}$ 和 $||\cdot||_{\beta}$，存在常数 $m$ 和 $M$，使得

$m \| x \| _ { \alpha } \leq \| x \| _ { \beta } \leq M \| x \| _ { \alpha }$

其中 $m$ 和 $M$ 不依赖于 $x$。例如，当 $x\in\mathbb{R}^n$

$\| x \| _ { 2 } \leq \| x \| _ { 1 } \leq \sqrt { n } \| x \| _ { 2 }$

这种等价性意味着，如果一个向量序列 $\left( x _ { i } \right) _ { i = 1 } ^ { \infty }$ 在一个范数中收敛到 $x^*$

$\lim\limits_ { i \rightarrow \infty } \left\| x _ { i } - x ^ { * } \right\| = 0$

那么它在所有范数中都收敛到相同的极限。

在数据挖掘应用中，通常使用两个向量之间*角度的余弦值*作为距离度量：

$\cos \theta ( x , y ) = \frac { x ^ { T } y } { \| x \| _ { 2 } \| y \| _ { 2 } }$

用这个方法，如果余弦值接近一，两个向量就很接近。同样，如果 $x$ 和 $y$ 之间的*夹角*为 $\pi/2$，即 $x^Ty=0$，则x和y是正交的。

## 2.4 矩阵范数

对于任何向量范数，我们都可以定义相应的算子范数。设 $\cdot$ 为向量范数。相应的*矩阵范数*定义为

$\| A \| = \sup\limits_ { x \neq 0 } \frac { \| A x \| } { \| x \| }$

可以证明这样的矩阵范数满足（对于 $\alpha \in \mathbb{R}$）

$\begin{aligned} \| A \| & \geq 0  \text{ for all } A \\ \| A \| &= 0 \text { if and only if } A = 0 \\ \| \alpha A \| & = | \alpha | \| A \| , \alpha \in \mathbb { R } , \\ \| A + B \| & \leq \| A \| + \| B \| , \text { 三角不等式 } \end{aligned}$

对于上面定义的矩阵范数，以下基本不等式成立。

**命题 2.1** *让 $\cdot $ 表示一个向量范数和相应的矩阵范数。然后*

$\begin{aligned} \| A x \| & \leq \| A \| \| x \| \\ \| A B \| & \leq \| A \| \| B \| \end{aligned}$

***证明***  根据我们的定义

$\frac { \| A x \| } { \| x \| } \leq \| A \|$

对于所有 $x\neq 0$ 的情况，得到第一个不等式。第二个通过使用前两个 $||ABx||$ 来证明。

我们可以证明*二次范数*满足

$\| A \| _ { 2 } = \left( \max\limits_ { 1 \leq i \leq n } \lambda _ { i } \left( A ^ { T } A \right) \right) ^ { 1 / 2 }$

即矩阵 $A^TA$ 最大特征值的平方根。因此，对于给定的矩阵 $||A||_2$（中等或大尺寸的矩阵），要获得的计算量相对较大。计算*矩阵无穷范数*（对于 $A\in\mathbb{R}^{m\times n}$ ）要容易得多。

$\| A \| _ { \infty } = \max\limits_ { 1 \leq i \leq m } \sum\limits_ { i = 1 } ^ { n } \left| a _ { i j } \right|$

矩阵*一次范数*

$\| A \| _ { 1 } = \max\limits_ { 1 \leq j \leq n } \sum\limits_ { i = 1 } ^ { m } \left| a _ { i j } \right|$

在第6.1节中，我们将看到矩阵的2次范数有一个关于 $A$ 的奇异值的显式表达式。

设 $A\in \mathbb{R}^{m\times n}$。在某些情况下，我们将把矩阵不当作一个线性算子，而是当作一个空间中的点，即 $\mathbb{R}^{mn}$。然后我们可以使用 *Frobinius* 矩阵范数，它由

$\| A \| _ { F } = \sqrt { \sum \limits_ { i = 1 } ^ { m } \sum \limits_ { j = 1 } ^ { n } a _ { i j } ^ { 2 } }$，式2.7

有时也用等价形式写出弗罗贝尼乌斯（ Frobeniu）范数。

$\| A \| _ { F } ^ { 2 } = \operatorname { tr } \left( A ^ { T } A \right)$，式2.8

其中矩阵 $B\in \mathbb{R}^{m\times n}$ 的*迹*是其对角元素的和，

$\operatorname { tr } ( B ) = \sum\limits_ { i = 1 } ^ { n } b _ { i i }$

弗罗贝尼乌斯范数不对应于向量范数，因此在这个意义上它不是一个算子范数。这个范数的优点是比2次范数更容易计算。弗罗贝尼乌斯*矩阵范数*实际上与欧几里得*向量范数*密切相关，即当矩阵用 $\mathbb{R}^{m\times n}$ 中的元素标识时，它是矩阵 $\mathbb{R}^{m\times n}$（线性空间）上的欧几里得向量范数。

## 2.5线性无关：基础部分

给定一组在 $\mathbb{R}^m $ 向量 $(v_j)^{n}_{j=1}$, 其中 $m\ge n$，考虑一组线性组合

$\operatorname { span } \left( v _ { 1 } , v _ { 2 } , \ldots , v _ { n } \right) = \left\{ y | y = \sum\limits_ { j = 1 } ^ { n } \alpha _ { j } v _ { j } \right\}$

对于任意系数 $\alpha_j$，向量 ${(}v_j{)}^{n}_{j=1}$ 称为*线性无关*的条件为

$\sum _ { j = 1 } ^ { n } \alpha _ { j } v _ { j } = 0 \text { if and only if } \alpha _ { j } = 0 \text { for } j = 1,2 , \ldots , n$

$ \mathbb{R}^m $ 中的一组 $m$ 线性无关向量称为 $\mathbb{R}^{m}$ 中的*基*：$\mathbb{R}^{m}$ 中的任何向量都可以表示为基向量的线性组合。

**命题2.2** *假设向量 $ {(}v_j{)}^{n}_{j=1} $ 是线性相关的。然后一些 $v_k$ 可以写成其余部分的线性组合，$v _ { k } = \sum _ { j \neq k } \beta _ { j } v _ { j }$。*

**证明。** *存在系数 $ \alpha_j $，其中一些 $\alpha_k\neq 0$，这样*

$\sum \limits_ { j = 1 } ^ { n } \alpha _ { j } v _ { j } = 0$

取 $\alpha_k \neq 0$，可以写成

$\alpha _ { k } v _ { k } = \sum\limits _ { j \neq k } - \alpha _ { j } v _ { j }$

等效成如下形式

$v _ { k } = \sum\limits _ { j \neq k } \beta _ { j } v _ { j }$， $\beta_j=-\alpha_j / \alpha_k$

如果我们有一组线性相关的向量，那么我们可以保持一个线性无关的子集，并用线性无关的子集来表示其余的部分。因此，我们可以将线性无关向量的个数作为集合信息内容的度量，并相应地压缩集合：以线性无关向量作为集合的代表（基向量），并根据基计算其余向量的坐标。然而，在实际应用中，我们很少有*精确的线性相关向量*，*大部分是线性相关向量*。结果表明，为了使这种*数据简化*过程实用且保持数值稳定，我们需要基向量不仅是线性无关的，而且要正交的。我们将在第4章中讨论这一点。

## 2.6 矩阵的秩

矩阵的*秩*定义为线性无关列向量的最大数目。线性无关列向量的个数等于线性无关行向量的个数是线性代数的标准结果。

稍后我们将看到，任何矩阵都可以表示为秩1矩阵的展开式。

**命题2.3** *外积矩阵 $xy^T$，其中 $x$ 和 $y$ 是 $\mathbb{R}^n $ 中的向量，秩为1。*

***证明***

$x y ^ { T } = \left( \begin{array} { l l l l } { y _ { 1 } x } & { y _ { 2 } x } & { \cdots } & { y _ { n } x } \end{array} \right) = \left( \begin{array} { c } { x _ { 1 } y ^ { T } } \\ { x _ { 2 } y ^ { T } } \\ { \vdots } \\ { x _ { n } y ^ { T } } \end{array} \right)$

因此，$xy^T$ 的所有列（行）都是线性相关的。

一个秩为 $n$ 的平方矩阵 $A \in \mathbb { R } ^ { n \times n }$ 称为非奇异矩阵，其*逆* $A^{−1}$ 满足

$A A ^ { - 1 } = A ^ { - 1 } A = I$

如果我们用一个非奇异矩阵乘以线性无关向量，那么这些向量就保持线性无关。

**命题2.4** *假设向量 $v_1, ..., v_p$ 是线性无关的。对于任何非奇异矩阵 $T$，向量  $Tv_1, ..., Tv_p$是线性无关的。*

**证明** 显然 $\sum _ { j = 1 } ^ { p } \alpha _ { j } v _ { j } = 0$，如果仅当 $\sum _ { j = 1 } ^ { p } \alpha _ { j } T v _ { j } = 0$ 时（因为我们可以用 $T$ 或 $T^{-1}$ 将任何方程相乘）。因此，声明如下。








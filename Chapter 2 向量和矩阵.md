# 第二章 向量和矩阵

我们将假设读者已知线性代数的基本概念。为了完整起见，这里将概括一些。

## 2.1 矩阵-向量乘法

如何定义线性代数中的基本操作很重要，因为它会影响一个人对抽象概念的心理图像。有时人们会认为操作应该以某种顺序完成，而事实上*这样的定义*并没有排序$^3$。 设 $A$ 是 $m\times n$矩阵。考虑矩阵-向量乘法的定义：

$y = A x , \quad y _ { i } = \sum _ { j = 1 } ^ { n } a _ { i j } x _ { j } , \quad i = 1 , \ldots , m$ ，式2.1

符号可以说明其定义

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

```bash
for i=1:m
    y(i)=0;
end
for j=1:n
    for i=1:m
    	y(i)=y(i)+A(i,j)*x(j);
    end
end
```

```bash
y(1:m)=0;
for j=1:n
	y(1:m)=y(1:m)+A(1:m,j)*x(j);
end
```

$A \in \mathbb { R } ^ { m \times k }$

$B \in \mathbb { R } ^ { k \times n }$

$\begin{aligned} \mathbb { R } ^ { m \times n } \ni C & = A B = \left( c _ { i j } \right) \\ c _ { i j } & = \sum _ { s = 1 } ^ { k } a _ { i s } b _ { s j } , \quad i = 1 , \ldots , m , \quad j = 1 , \ldots , n \end{aligned}$

```bash
for i=1:m
  for j=1:n
    for s=1:k
      C(i,j)=C(i,j)+A(i,s)*B(s,j)
    end
  end
end
```

```bash
for i=1:m
  for j=1:n
	C(i,j)=A(i,1:k)*B(1:k,j)
  end
end
```

```bash
for ...
  for ...
    for ...
      C(i,j)=C(i,j)+A(i,s)*B(s,j)
    end
  end
end
```

```bash
for j=1:n
  for s=1:k
	C(1:m,j)=C(1:m,j)+A(1:m,s)*B(s,j)
  end
end
```


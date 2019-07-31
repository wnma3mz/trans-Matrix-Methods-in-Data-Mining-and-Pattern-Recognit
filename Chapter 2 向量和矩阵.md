# 向量和矩阵



$y = A x , \quad y _ { i } = \sum _ { j = 1 } ^ { n } a _ { i j } x _ { j } , \quad i = 1 , \ldots , m$



$\left( \begin{array} { l } { \times } \\ { \times } \\ { \times } \\ { \times } \end{array} \right)=\left( \begin{array} { c c c c } { \leftarrow } & { - } & { - } & { \rightarrow } \\ { \leftarrow } & { - } & { - } & { \rightarrow } \\ { \leftarrow } & { - } & { - } & { \rightarrow } \\ {\leftarrow } & { - } & { - } & { \rightarrow } \end{array} \right) \left( \begin{array} { l } { \uparrow } \\ { | } \\ { | }  \\ { \downarrow } \end{array} \right)$

```bash
for i=1:m
  y(i)=0;
  for j=1:n
    y(i)=y(i)+A(i,j)*x(j);
  end
end
```

$y = A x = \left(\begin{array} { c c c c } { a _{ 1 } } & { a _{ .2 } } & { \cdots } & { a _{ . n } } \end{array} \right) \left(\begin{array} { c } { x _{ 1 } } \\ { x _{ 2 } } \\ { \vdots } \\ { x _{ n } } \end{array} \right) = \sum\limits_{ j = 1 } ^ { n } x _{ j } a _{ . . j }$

$\left( \begin{array} { l } { \uparrow } \\ { | } \\ { | }  \\ { \downarrow } \end{array} \right)=\left( \begin{array} { l l l l } { \uparrow } & { \uparrow } & { \uparrow } & { \uparrow } \\ { | } & { | } & { | } & { | } \\ { | } & { | } & { | } & { | } \\ { \downarrow } & { \downarrow } & { \downarrow } & { \downarrow } \end{array} \right)\left( \begin{array} { l } { \times } \\ { \times } \\ { \times } \\ { \times } \end{array} \right) $

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

